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
This is an example of how to download the *Frames* mini dataset using the `zod` CLI tool.
```
pip install zod[cli]
zod download --url <url/to/shared/dropbox/folder> --ourput-dir <path/to/output/dir> frames --mini
```
and this is how you would download the sequences mini dataset:
```
pip install zod[cli]
zod download --url <url/to/shared/dropbox/folder> --ourput-dir <path/to/output/dir> sequences --mini
```