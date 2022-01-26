# Homework 1


### Google version
```
google-cloud-sdk % gcloud -v
Google Cloud SDK 370.0.0
bq 2.0.73
core 2022.01.21
gsutil 5.6
```

#### or

```
alia@MacBook-Air-Alia google-cloud-sdk % gcloud --version
Google Cloud SDK 370.0.0
bq 2.0.73
core 2022.01.21
gsutil 5.6
```
### Terraform apply output

```
terraform apply
```

```
Your GCP Project ID

  Enter a value: global-booster-339410

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following
symbols:

  + create

Terraform will perform the following actions:


# google_bigquery_dataset.dataset will be created
  + resource "google_bigquery_dataset" "dataset" {
      + creation_time              = (known after apply)
      + dataset_id                 = "trips_data_all"
      + delete_contents_on_destroy = false
      + etag                       = (known after apply)
      + id                         = (known after apply)
      + last_modified_time         = (known after apply)
      + location                   = "europe-west6"
      + project                    = "global-booster-339410"
      + self_link                  = (known after apply)

      + access {
          + domain         = (known after apply)
          + group_by_email = (known after apply)
          + role           = (known after apply)
          + special_group  = (known after apply)
          + user_by_email  = (known after apply)

          + view {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + table_id   = (known after apply)
            }
        }
    }

  # google_storage_bucket.data-lake-bucket will be created
  + resource "google_storage_bucket" "data-lake-bucket" {
      + force_destroy               = true
      + id                          = (known after apply)
      + location                    = "EUROPE-WEST6"
      + name                        = "dtc_data_lake_global-booster-339410"
      + project                     = (known after apply)
      + self_link                   = (known after apply)
      + storage_class               = "STANDARD"
      + uniform_bucket_level_access = true
      + url                         = (known after apply)

      + lifecycle_rule {
          + action {
              + type = "Delete"
            }

          + condition {
              + age                   = 30
              + matches_storage_class = []
              + with_state            = (known after apply)
            }
        }

      + versioning {
          + enabled = true
        }
    }
Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

google_bigquery_dataset.dataset: Creating...
google_storage_bucket.data-lake-bucket: Creating...
google_storage_bucket.data-lake-bucket: Creation complete after 1s [id=dtc_data_lake_global-booster-339410]
google_bigquery_dataset.dataset: Creation complete after 2s [id=projects/global-booster-339410/datasets/trips_data_all]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```
### Count records

```
SELECT COUNT(1)
FROM yellow_taxi_trips
WHERE date(tpep_pickup_datetime) = '2021-01-15'

```
###  Largest tip for each day


```
SELECT CAST(tpep_pickup_datetime AS DATE) as date, MAX(tip_amount) as tip
FROM yellow_taxi_trips
GROUP BY date
ORDER BY tip DESC
LIMIT 1

```

