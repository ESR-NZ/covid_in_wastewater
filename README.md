# Aotearoa New Zealand Wastewater COVID-19 Surveillance Programme

This GitHub repo provides data sets used to support the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) wastewater COVID-19 surveillance programme (https://www.esr.cri.nz/our-expertise/covid-19-response/wastewater-testing-results). This includes for the current [wastewater dashboard](https://poops.nz/) and [historical dashboard](https://historic.poops.nz/). Data are SARS-CoV-2 RNA quantitation in wastewater, reported COVID-19 case data, and geographic metadata.

Funding for the dashboard and data repository is provided by the [Ministry of Health](https://www.health.govt.nz/).

## About the Data

The wastewater COVID-19 surveillance programme was first launched to monitor the presence of COVID-19 in Aotearoa New Zealand. This aided our ability to identify the presence of COVID-19 in the community. Once COVID-19 was endemic in New Zealand, the programme was used to monitor SARS-CoV-2 RNA levels and variants in communities. The methods used to recover and detect SARS-CoV-2 in wastewater are described in [Hewitt et al 2022](https://www.sciencedirect.com/science/article/pii/S0043135421012264).

The selection of wastewater sites has been based on several factors, including the stage of the pandemic, population, and geographic coverage. Both sites and sample frequency vary over time. Typically, samples are collected twice per week from larger wastewater catchments. In periods where wastewater was collected from smaller towns and communities, the frequency may have been once a week.

Most samples are collected by an autosampler. Autosamplers collect a small volume of wastewater at regular intervals over the course of a 24-hour period. From July 2024, all wastewater samples were collected using autosamplers. When composite samplers were not available, 'grab' samples were collected. Most grab samples were taken at a single point in time. Grab samples may not be as representative as a 24-hour composite sample. More variation may be expected with grab samples, samples collected from smaller catchments (as an individual case can have a disproportionately large effect on overall viral level in small catchments), and from sites that are only sampled once per week.

The catchment polygons are not included. They are the intellectual property of the individual regional and city councils that operate the treatment plants. Some are available publicly, otherwise if you are interested in obtaining specific GIS files for a site, we suggest contacting the relevant council.

## Wastewater Data

The wastewater data shows the SARS-CoV-2 genome copies per litre (see lab analysis and methodology for more details). To preserve anonymity of sites with small populations, these have been excluded from the site-specific data. These are still included in the aggregated regional and national wastewater data.

### Site Aggregation

For each sample location, if more than one sample was taken, this is averaged to determine the average genome copies per person per day for the site that week. This is then normalised using population and wastewater flow to give SARS-CoV-2 genome copies per person per day.

### Regional Aggregation

For the regional aggregated data, the averaged and normalised site data is aggregated using a weighted mean. The weight applied to each site is calculated using site population divided by region population (for that week) making the site results proportional to the regional population. This weighting ensured that small catchments are not over-represented and large catchments are not under-represented in the regional aggregation. A 7-day average of genome copies/person/day is reported for Monday-Sunday.

### National Aggregation

For the national aggregated data, each week the averaged and normalised site data is aggregated using a weighted mean. The weight applied was calculated using site population divided by national population (for that week). This weighting, like the regional aggregated data, ensures small catchments were not over-represented and large catchments under-represented. A 7-day average of genome copies/person/day is then reported for Monday-Sunday.

## Reported Case Data

Reported case numbers are calculated by summing up all the new reported cases to the Ministry of Health for that week. Cases are reported on a per-day basis because wastewater samples are generally representative of the viral load in the catchment for the preceding 24-hrs. The report date is aligned with what the Ministry of Health publishes on their website. The average number of new COVID-19 cases reported per day via NCTS or [EpiSurv](https://www.phfscience.nz/expertise/public-health/health-information-systems/#EpiSurvnotifiablediseasedatabase) is used. When the report date is not available, the first non-null value from the fields onset date, lab sample date, lab confirmed detection date, or earliest date is used.

## Folder Structure

- `/data`: contains data for reduced sites tested from July 2024
- `/historic_data`: contains data for all sites tested from week ending 11 July 2021 till June 2024

## Data Dictionary

### National Data

**cases_national.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `case_7d_avg`: average number of new COVID-19 reported cases reported per day using reported date. If not available, then the first non-null value for onset date, lab sample date, lab confirm detection, or earliest date.

**ww_national.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `national_population`: the sum of catchment populations covered by testing that week.
- `copies_per_person_per_day`: average of the SARS-CoV-2 genome copies per person per day. Calculated as an average of results from the previous 7 days and normalised by catchment for population covered by i) catchment for population covered by testing and ii) wastewater flow into the wastewater treatment plant (WWTP) per day.

### Regional Data

**cases_regional.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `Region`: region name.
- `case_7d_avg`: average number of new COVID-19 reported cases per day using reported date. If not available, then the first non-null value for onset date, lab sample date, lab confirm detection, or earliest date.

**ww_regional.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `Region`: region name.
- `copies_per_person_per_day`: average of the SARS-CoV-2 genome copies per person per day. Calculated as an average of results from the previous 7 days. SARS-CoV-2 genome copies results are normalised by i) catchment for population covered by testing and ii) wastewater flow into the WWTP per day.
- `n_site`: number of sites within the region contributing to each week's data.

### Site Data

**cases_site.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `SampleLocation`: wastewater testing site name, with two-letter region code, underscore, site name (e.g., "AU_Rosedale").
- `copies_per_person_per_day`: average of the SARS-CoV-2 genome copies per person per day. Calculated as an average of results from the previous 7 days. SARS-CoV-2 genome copies results are normalised by i) catchment for population covered by testing and ii) wastewater flow into the WWTP per day.

**ww_site.csv**

- `week_end_date`: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).
- `SampleLocation`: wastewater testing site name (e.g., "AU_Rosedale").
- `case_7d_avg`: An average of the SARS-CoV-2 genome copies per person per day. SARS-CoV-2 genome copies results are normalised by catchment for population covered by testing and wastewater flow per day. Calculated as an average of results from the previous 7 days.

**sites.csv**

- `SampleLocation`: wastewater testing site name, with two-letter region code, underscore, site name (e.g., "AU_Rosedale").
- `DisplayName`: display name used for reporting (e.g., "Rosedale").
- `SampleType`: sampling method used; autosampler or grab.
- `Latitude`: the latitude of the sampling location, typically a wastewater treatment plant.
- `Longitude`: the longitude of the sampling location, typically a wastewater treatment plant.
- `Population`: the estimated population covered by the wastewater catchment area.
- `Region`: name of the region that site is located in.
- `shp_label`: a unique identifier for the catchment polygons.

**variants_last_two_weeks.csv**

- `variant`: variant name.
- `DisplayName`: site display name used on the variants chart.
- `detected`: boolean (`true` or `false`) to indicate whether the variant was detected.

*Note:* Wastewater samples often contain a mixture of SARS-CoV-2 variants from many infected individuals. The results show the percentage of variants detected at the national level. The percentage of each variant in wastewater is a proxy for the prevalence of each variant in the community. Up to July 2024, variant analysis was performed on a subset of samples from select wastewater sites. Since July 2024, all sites sampled are tested for variants. National variant proportions are calculated as the mean of the sites weighted by site population.

For further guidance, please refer to the 'Estimated variant prevalence' notes on the [wastewater dashboard](https://www.poops.nz/).

## Raw Wastewater Data

**ww_data_all.csv**

- `SampleLocation`: wastewater testing site name, with two-letter region code, underscore, site name (e.g., "AU_Rosedale").
- `sars_gcl`: The amount of SARS-CoV-2 genome copies per litre of wastewater.
- `Result`: Either "Detected" if SARS-CoV-2 was identified in the wastewater sample or "Not detected".
- `copies_per_person_per_day`: average of the SARS-CoV-2 genome copies per person per day. Calculated as an average of results from the previous 7 days. SARS-CoV-2 genome copies results are normalised by i) catchment for population covered by testing and ii) wastewater flow into the WWTP per day.

## Laboratory Methodology

Samples are sent from each enrolled wastewater treatment plant to PHF Science. Processing first involves separating the solids from liquid by centrifugation, followed by eluting the virus from the solids. The virus from the solids is then combined with that in the liquid phase and concentrated to a small volume by polyethylene glycol (PEG) precipitation. The viral RNA is extracted. The presence of SARS-CoV-2 RNA in the sample is then determined using RT-qPCR (reverse transcription-quantitative polymerase chain reaction) with the N-gene of the SARS-CoV-2 viral genome. SARS-CoV-2 RNA is considered detected when any of the RT-qPCR replicates are positive. A result of "Not detected" means that SARS-CoV-2 RNA is either absent from the sample or at a level in the wastewater that is too low to be detected.

When SARS-CoV-2 RNA is detected by RT-qPCR, the concentration in the sample is calculated and converted from genome copy per reaction into genome copies per litre of wastewater. The unit conversion considers the initial sample volume, final volume of the concentrate used for RNA extraction, final volume of the eluted RNA, and amount of RNA used in the RT-qPCR template. Low amounts of SARS-CoV-2 RNA in a sample may not be accurately quantified and are recorded as 500 genome copies/L.

## Citation

If you would like to use this data, please cite: COVID-19 Data Repository by the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science), and the URL: <https://github.com/ESR-NZ/covid_in_wastewater>

For academic publications, cite the following paper:

> Hewitt, Joanne, et al. "Sensitivity of wastewater-based epidemiology for detection of SARS-CoV-2 RNA in a low prevalence setting." *Water Research* 211 (2022): 118032. <https://doi.org/10.1016/j.watres.2021.118032>

## Acknowledgements

This work represents the combined efforts of many individuals and organisations. We thank the teams across the country who collect the wastewater and associated metadata that underpins this work.

PHF Science acknowledges the support of councils and wastewater providers across New Zealand who provide us with samples and staff in the public health services in New Zealand who provide us with data from their regions. This work is funded by the Ministry of Health.

## Terms of Use

1. This dataset is owned by the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) and licensed for reuse under the [Creative Commons Attribution 4.0 International licence](https://creativecommons.org/licenses/by/4.0/). This license means that you are free to copy, distribute and adapt the material, as long as you attribute it to the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) and abide by the other license terms. This license does not apply to any logos and trademarks on this website – these specific elements may not be reused without the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) prior written consent.
2. If you wish to use the data, you must attribute it as the "COVID-19 Data Repository by the New Zealand Institute for Public Health and Forensic Science Ltd", and the URL: <https://github.com/ESR-NZ/covid_in_wastewater>
3. You may use our application programming interface ("API") to facilitate access to the dataset, whether through a separate website or through another type of software application.
4. You may not represent or imply that the New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) has approved or endorsed the manner or purpose of your use or reproduction of the dataset.
5. The New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) reserves the right at any time in its sole discretion to modify or discontinue (temporarily or permanently) this website, the dataset, and any means of accessing the dataset, with or without prior notice to you.

## Disclaimer

Data is shared solely for the benefit of the New Zealand Ministry of Health, Public Health Service Providers and other Third Party Beneficiaries as defined in the Contract between PHF Science and the MoH. PHF Science does not accept any legal liability or responsibility for use of information contained in this repository by any other person or organisation.

## About PHF Science

The New Zealand Institute for Public Health and Forensic Science Ltd (PHF Science) is a New Zealand Government-owned research organisation dedicated to enhancing the
health, wellbeing and safety of our communities. Specialising in public health and forensic sciences, we monitor disease, help ensure safe food and water, reduce harm from drugs, support the justice system and more. Our science powers innovations and solutions to help New Zealand prosper and grow.
