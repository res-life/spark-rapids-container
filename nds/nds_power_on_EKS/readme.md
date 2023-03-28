This document describes how to run 'nds_power.py` on EKS

# parameter files
## parameter
e.g.:
```
s3://ndsv2-data/parquet_sf1000 time-123.csv --output_prefix s3://chongg/test/tmp --json_summary_folder 500 --keep_sc
```
`s3://ndsv2-data/parquet_sf1000` parameter is `input_prefix`
`time-123.csv` parameter is `time_log`
`s3://chongg/test/tmp` parameter is `output_prefix`
`500` parameter is `json_summary_folder`
Note: please do not specify `property_file`, currently not support this parameter.
For more details, refer to the parameters in the `nds_power.py` file

## query_0.sql
This file is the stream file.
For how to generate stream file, refer to the README file in the root source folder.

# create NDS zip file and put it into S3
```
cd spark-rapids-benchmarks
zip -r nds.zip nds
aws s3 cp nds.zip s3://path/to/this/zip
```

# run nds_power on notebook
```
spark.sparkContext.addPyFile("s3://path/to/this/zip")
from nds import nds_power
nds_power.run_query_stream_on_EKS()
```