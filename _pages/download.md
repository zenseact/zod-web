---
permalink: /download/
title:  "Download"
categories: jekyll update
---
<br>

# Downloading ZOD
We have made the ZOD available for download through a shared Dropbox folder. To download the dataset, you need to request access to the folder. Once you have been granted access, you can download the dataset using the command line interface (CLI) tool. The CLI tool, along with an extensive development kit, can be found on Github [here](https://github.com/zenseact/zod).
## Requesting access
If you are interested in using ZOD, we kindly ask you to request access by emailing us at <opendataset@zenseact.com>. Your request should include the following information:
- Your name
- Your affiliation
- Your email address connected to your Dropbox account
- A short description of your intended use of the dataset.

Please feel free to use the template below as a starting point for your request:
```
Dear Zenseact,

I am interested in using the Zenseact Open Dataset (ZOD) for my research and I would like to request access to the dataset.
Please find the requested information below:

Name: <your name>
Affiliation: <your affiliation>
Email: <your email address>
Intended use: <short description of your intended use of the dataset>

Best regards,
<your name>
```

Once we have received your request, we will review it and get back to you as soon as possible with a link to the Dropbox folder that should be used together with the downloading script provided in the `zod` CLI interface.


## Download using the CLI
The following will install the `zod` CLI tool and start an interactive downloading process:
```bash
pip install zod[cli]
zod download
```
This will prompt you for the required information, present you with a summary of the download, and then ask for confirmation. You can of course also specify all the required information directly on the command line, and avoid the confirmation using `--no-confirm` or `-y`. For example:
```bash
zod download -y --url="<download-link>" --output-dir=<path/to/outputdir> --subset=frames --version=mini
```
By default, all data streams are downloaded for ZodSequences and ZodDrives. For ZodFrames, DNAT versions of the images, and surrounding (non-keyframe) lidar scans are excluded. To download them as well, run:
```bash
zod download -y --url="<download-link>" --output-dir=<path/to/outputdir> --subset=frames --version=full --num-scans-before=-1 --num-scans-after=-1 --dnat
```
If you want to exclude some of the data streams, you can do so by specifying the `--no-<stream>` flag. For example, to download only the DNAT images, infos, and annotations, run:
```bash
zod download --dnat --no-blur --no-lidar --no-oxts --no-vehicle-data
```
Finally, for a full list of options you can of course run:
```bash
zod download --help
```
