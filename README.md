# Benchmark geospatial query speed on NoSQL(-like) databases

## Test databases

- [MongoDB](https://www.mongodb.com/)
- [Redis](https://redis.io/)

## Test language and lib

- [TypeScript](https://www.typescriptlang.org/)
  - [Mongoose](https://mongoosejs.com/)

## Test Host Environment

- [GitHub Codespaces](https://docs.github.com/en/codespaces)
- [GitHub Actions](https://docs.github.com/en/actions)

## Test dataset

By default, this benchmark uses [iNaturalist 2017](https://www.kaggle.com/c/inaturalist-challenge-at-fgvc-2017)'s [Fine Grained Geolocation Datasets (visipedia/fg_geo)](https://github.com/visipedia/fg_geo). Which contains 654,818 records of geolocation point.

File was placed at `datasets/inat2017/inat2017_file_name_to_geo.csv`.

Format:

```csv
filename,latitude,longitude
```

We also provide 3 other runtime generated datasets:

- Random
  - Points are totally placed by RNG.
- Grid
  - Points separated evenly around the earth.
  - Using [Fibonacci sphere algorithm](https://arxiv.org/abs/0912.4540).
- Cluster
  - Every 50 points will be placed together with a bit offset as a cluster, and all clusters will be placed randomly.

## Test queries

- Data should be loaded into the database before running the queries.
  - Up to 1 minute for preparation before running query.
    - Warm up is not allowed at this time.
- Storage cost will be calculated.
  - For memory-storage databases, both memory and persist storage cost will be calculated.
- In theory, all databases should return the same result.

Basic test requires all queries runs one by one in a single process/thread.
Advanced test allows queries to run in parallel, and allows to optimized for test host.

### Query A: Find nearest location

Pick a random location, find the closest location in the dataset.

Query will be run 10000 times.

### Query B: Find locations within a radius

Pick a random location from the dataset, find all locations within certain distance.

Query will be run 5000 times.

### Query C: Find locations within a radius and order them.

Pick a random location from the dataset, find all locations within certain distance, order by distance.

Query will be run 5000 times.

## License and Citation

This project is licensed under the terms of the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license.

Citation info can be found at [CITATION.cff](./CITATION.cff)
