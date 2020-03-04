# PEPATAC QC PEP


The `paqc.yaml` file is the working PEP for these samples.
The `paqc_annotation.csv` file is the working annotation file for these samples.

## Download data

Get source samples using geofetch
```
geofetch -i accessions.txt -n paqc --m paqc_geo_metadata
```

You can set up a default sratoolkit config like this:

```
export DATA="..."
echo "/repository/user/main/public/root = \"$DATA\"" > ${HOME}/.ncbi/user-settings.mkfg
```

## Format your PEP

You'll need to manually tweak the output of geofetch to adopt the new PEP 2.0.0 specification. Validate the configuration file with [`peppy`](https://github.com/pepkit/peppy) like so:
```
peppy validate paqc.yaml -s http://schema.databio.org/pipelines/pepatac.yaml
```

## Convert the SRA files to FASTQ

Use the `sra_convert` amendment to point at the conversion pipeline. Run in looper:
```
PROCESSED=/project/shefflab/processed DATA=/project/shefflab/data/ looper run paqc.yaml --amendments sra_convert
```

## Run PEPATAC

```
PROCESSED=/project/shefflab/processed DATA=/project/shefflab/data/ looper run paqc.yaml -d
```

The `peppro_paper.yaml` file is the working PEP for these samples.
The `peppro_paper.csv` file is the working annotation file for these samples.
