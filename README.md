# Singularity Images Repository

This repository contains Singularity definition files for various bioinformatics tools and utilities, with automated builds and deployment to Sylabs Cloud Library.

## Structure

Tools are organized in directories following the pattern `toolname_version`:

```
├── bioconductor_4.0/
│   └── Singularity.def
├── bcftools_1.9/
│   └── Singularity.def
└── gatk_4.2/
    └── Singularity.def
```

## Automated Workflow

The GitHub Actions workflow automatically:
- Detects changes to any `toolname_version/Singularity.def`
- Builds the Singularity image as `toolname_version.sif`
- Pushes to Sylabs Cloud Library as `username/toolname:version`

**Example**: `bioconductor_4.0/` → `library://username/bioconductor:4.0`
Example `Singularity.def`:

```singularity
Bootstrap: docker
From: ubuntu:20.04

%labels
    Author your.email@domain.com
    Version 1.0

%help
    This container provides [tool description]

%post
    # Install dependencies
    apt-get update && apt-get install -y \
        build-essential \
        wget \
        curl

    # Install your tool
    # ... installation commands ...

%environment
    export PATH=/usr/local/bin:$PATH

%runscript
    exec "$@"
```

## Usage

Once deployed, images can be pulled and used locally:

```bash
# Pull from Sylabs Cloud
singularity pull library://username/toolname:version

# Run the tool
singularity exec toolname_version.sif your-command
```
