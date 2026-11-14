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

For Assignment 2, we used Lorimer's _Gazetteer of the Persian Gulf, Oman and Central Arabia_ to investigate the question: **How many houses does the Gazetteer record in the Trucial States?** We explored this question by combining historical text, structured CSV data, geographic filtering, and an interactive map.

## What we investigated

The dataset contains locations and references to houses recorded in the Gazetteer. Since the source covers a broad region, the initial data included places outside the area relevant to our question. We therefore needed to identify a practical geographic study area before interpreting the mapped results.

We also treated each row as a documented record rather than automatically treating it as a separate settlement or an independent population count. Several rows can refer to the same location while describing different families, units, or overlapping totals.

## Methods

We used the following process:

- Loaded the original CSV dataset into a Python mapping workflow
- Plotted the latitude and longitude coordinates with Kepler.gl
- Defined a preliminary study area using a geographic bounding box
- Filtered the dataset by minimum and maximum latitude and longitude
- Extracted recorded house values from the associated Gazetteer text
- Preserved contextual information such as units, scope, source articles, and page references
- Created an interactive map from the filtered and enriched records

One important technical lesson was that drawing a GeoJSON boundary does not automatically filter the records displayed on a map. The original dataframe continued to contain every location, so we had to apply the coordinate filter to the data itself before exporting the bounded CSV and passing it to Kepler.gl.

## What we found

The mapped records were concentrated along the coast, particularly around Abu Dhabi, Dubai, Sharjah, and Ras Al Khaimah. Liwa was a notable inland exception, with a less dense pattern of recorded houses.

These patterns may relate to coastal economic activity, including pearl fishing, fishing, and trade. The houses recorded in Liwa may instead be connected to the agricultural possibilities of the oasis. These interpretations remain provisional because the map shows recorded houses, not a complete population census.

## Limitations

The rectangular bounding box is only an approximation of the historical Trucial States. It includes a practical geographic area for initial analysis but does not establish historical boundaries. In addition, the Gazetteer may omit settlements or provide estimates and ranges rather than precise counts.

The extraction process also depended on LLM-assisted reading of a large historical text. Although the PDF was generally machine-readable, some passages required OCR, and the extracted values were not independently checked against every original passage. The project therefore demonstrates both the usefulness and the risks of distant reading.

[Read the full Assignment 2 analysis]({{ '/assignment-2/' | relative_url }})
