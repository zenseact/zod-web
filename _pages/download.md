---
permalink: /download/
title:  "Download"
categories: jekyll update
---
<br>

# Downloading ZOD
We have made the ZOD available for download through a shared Dropbox folder. To download the dataset, you need to request access to the folder. Once you have been granted access, you can download the dataset using the command line interface (CLI) tool outlined in [Docs](/docs).
## Requesting access
If you are interested in using ZOD, we kindly ask you to requesting access by emailing us at <opendataset@zenseact.com>. Your request should include the following information:
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


## Downloading using the CLI

The following will install the `zod` CLI tool and download the mini dataset for initial testing and exploration:

```
pip install zod[cli]
zod download --url <url/to/shared/dropbox/folder> --output-dir <path/to/output/dir> --rm frames --mini
```

To download the full ZodFrames dataset, just drop the `--mini` flag:

```
zod download --url <url/to/shared/dropbox/folder> --output-dir <path/to/output/dir> --rm frames
```

The following flags can download additional parts of the dataset (note that the storage requirements can increase significantly):
- `--num-scans-before=-1` will download 10 scans before each core frame.
- `--num-scans-after=-1` will download 10 scans after each core frame.
- `--dnat` will download the images with DNAT (deep-fake) anonymization.
