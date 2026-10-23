# flower-data

Data registry for the [MLOps-portfolio](https://github.com/elisha-t-kdg/MLOps-portfolio) project.
This repository contains **no images in Git**: the raw dataset is versioned with
[DVC](https://dvc.org) and stored in a local DVC remote. Git only stores the
`flower_photos.dvc` pointer file (hash + metadata).

## Dataset

**Flower Photos**, published by TensorFlow:
https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz

3,670 photos in 5 classes:

| Class      | Images |
|------------|-------:|
| daisy      | 633    |
| dandelion  | 898    |
| roses      | 641    |
| sunflowers | 699    |
| tulips     | 799    |

The photos are licensed under CC-BY; see `flower_photos/LICENSE.txt` for the
attribution per image.

## Structure
```
flower-data/
├── .dvc/              # DVC configuration (incl. remote)
├── flower_photos.dvc  # pointer to the dataset version (tracked by Git)
└── flower_photos/     # the images (tracked by DVC, ignored by Git)
  ├── daisy/
  ├── dandelion/
  ├── roses/
  ├── sunflowers/
  └── tulips/
```


## Versions

| Tag  | Description                          |
|------|--------------------------------------|
| v1.0 | Original, unmodified raw dataset     |

## Usage

Get the data in this repository:

```bash
git clone https://github.com/elisha-t-kdg/flower-data.git
cd flower-data
dvc pull
```

Use it in another project (how MLOps-portfolio consumes it):

```bash
dvc import https://github.com/elisha-t-kdg/flower-data flower_photos -o data/raw/flower_photos --rev v1.0
```

> The DVC remote is local (`C:\KDG\dvc-storage\flower-data`), so `dvc pull`
> and `dvc import` only work on the machine where that storage exists.
