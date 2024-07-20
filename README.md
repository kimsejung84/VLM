# VLM_Datapipeline

This repository provides a data pipeline for Vision Language Models, specifically designed to process WorldView-3 imagery into 1024x1024 patches. Each patch retains its metadata, including latitude and longitude coordinates. The pipeline is capable of calculating the proportion of no-data pixels and determining the new central latitude and longitude for each patch. These processed WorldView-3 patches are stored in the NAS directory, while the corresponding text data is saved in a PostgreSQL database. For security purposes, the metadata is subsequently removed from each patch.

# Flow


# Docker


# Details
1. All in-house World View3 TIFF and TIF files
2. Patch Size: 1024x1024
- If the remaining area after cropping is smaller than 1024x1024, crop to 1024x1024 even if it results in overlapping patches.
- If the original size is smaller than 1024x1024, crop to the original size.
- Retain the band value of the original file as .RasterCount and exclude patches with a band value less than 3.
- Ensure patches are cut from the original without overlapping starting points.
3. Calculate the no-data value of the patch:
- Count the number of pixels with values 0 or 65535.
- Determine the percentage of no-data pixels relative to the total number of pixels in the patch.
4. Calculate the central coordinates of the patch.
