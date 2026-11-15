---
title: "Assignment 2: Mapping Houses in Lorimer's Gazetteer"
date: 2026-11-14
categories:
  - assignments
tags:
  - digital humanities
  - GIS
  - distant reading
  - historical geography
  - Lorimer's Gazetteer
excerpt: "An exploratory mapping project examining recorded houses in the Trucial States using Lorimer's Gazetteer, CSV data, Python, and Kepler.gl."
---

_Note: This post was generated with the help of Generative A.I. (GitHub Copilot and Claude) as a summary of Assignment #2._

For Assignment 2, we used Lorimer's _Gazetteer of the Persian Gulf, Oman and Central Arabia_ to investigate the question: **How many houses does the Gazetteer record in the Trucial States?** We explored this question by combining historical text, structured CSV data, geographic filtering, and an interactive map. The original dataset is available as the [Lorimer Gazetteer CSV]({{ '/assets/images/assignment2/data/lorimer-gazetteer-1-0.csv' | relative_url }}).

## What we investigated

The dataset contains locations and references to houses recorded in the Gazetteer. Since the source covers a broad region, the initial data included places outside the area relevant to our question. We therefore needed to identify a practical geographic study area before interpreting the mapped results.

We also treated each row as a documented record rather than automatically treating it as a separate settlement or an independent population count. Several rows can refer to the same location while describing different families, units, or overlapping totals.

## Methods

We used the following process:

- Loaded the [original CSV dataset]({{ '/assets/images/assignment2/data/lorimer-gazetteer-1-0.csv' | relative_url }}) into a Python mapping workflow
- Plotted the latitude and longitude coordinates with Kepler.gl
- Defined a preliminary study area using a geographic bounding box from [Klokan's Bounding Box Tool](https://boundingbox.klokantech.com/), following advice from our professor
- Filtered the dataset by minimum and maximum latitude and longitude
- Extracted recorded house values from the associated Gazetteer text
- Created a [bounded CSV]({{ '/assets/images/assignment2/data/lorimer-gazetteer-bounded.csv' | relative_url }}) containing only records inside the selected coordinates
- Used Claude to analyse the associated text and produce a [houses CSV]({{ '/assets/images/assignment2/data/lorimer-gazetteer-houses.csv' | relative_url }}) with the extracted house values
- Created an [interactive map]({{ '/assets/images/assignment2/data/lorimer-gazetteer-map.html' | relative_url }}) from the filtered and enriched records

One important technical lesson was that drawing a GeoJSON boundary does not automatically filter the records displayed on a map. The original dataframe continued to contain every location, so we had to apply the coordinate filter to the data itself before exporting the bounded CSV and passing it to Kepler.gl.

The workflow also showed the importance of checking each stage, even when generated code appeared to work. In retrospect, we should have included a data dictionary explaining the columns and their values. We relied on our familiarity with the tables and on LLM-assisted scripting, which made that omission easier to overlook.

## What we found

The mapped records were concentrated along the coast, particularly around Abu Dhabi, Dubai, Sharjah, and Ras Al Khaimah. Liwa was a notable inland exception, with a less dense pattern of recorded houses.

These patterns may relate to coastal economic activity, including pearl fishing, fishing, and trade. The houses recorded in Liwa may instead be connected to the agricultural possibilities of the oasis. These interpretations remain provisional because the map shows recorded houses, not a complete population census.

## Limitations

The rectangular bounding box is only an approximation of the historical Trucial States. It includes a practical geographic area for initial analysis but does not establish historical boundaries. In addition, the Gazetteer may omit settlements or provide estimates and ranges rather than precise counts.

The extraction process also depended on LLM-assisted reading of a large historical text. Although the PDF was generally machine-readable, some passages required OCR, and the extracted values were not independently checked against every original passage. The project therefore demonstrates both the usefulness and the risks of distant reading.

[Read the full Assignment 2 analysis]({{ '/assignment-2/' | relative_url }})

## References

- Broman, K. W., & Woo, K. H. (2018). [Data organization in spreadsheets](https://doi.org/10.1080/00031305.2017.1375989). _The American Statistician, 72_(1), 2–10.
- Harris, T. (1977). [The Liwa Oasis](https://enhg.org/bulletin/b02/02_11.HTM). _Emirates Natural History Group Bulletin_, 2.
- Lorimer, J. G. (1908). [Gazetteer of the Persian Gulf, ‘Oman and Central Arabia](https://archive.org/details/in.ernet.dli.2015.206964). Vol. 2, Geographical and Statistical.
- Barakat, N., & Wrisley, D. J. (Eds.). (2026). [A dataset of place names from J.G. Lorimer’s Gazetteer](https://doi.org/10.5281/zenodo.20122587) (Version 1.0).
