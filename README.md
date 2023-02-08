# Aotearoa Wastewater Surveillance Programme

This git repo provides data sets used to support The Institute of Environmental Science & Research (ESR) [wastewater surveillance programme](https://www.esr.cri.nz/our-expertise/covid-19-response/wastewater-testing-results) testing for SARS-CoV-2 and [wastewater dashboard](https://esr-cri.shinyapps.io/wastewater/). We provide wastewater SARS-CoV-2 concentrations, associated clinical case data and geographic metadata.

Funding for the dashboard and data repository was provided by the [Ministry of Health](https://www.health.govt.nz/).

## About the data

The SARS-CoV-2 wastewater surveillance programme was launched to monitor and track potential cases of COVID-19 in Aotearoa. From 2020 this has aided Aotearoa's ability to identify potential outbreaks and is now being used to track viral load in communities and monitor variants. The methods used for the identifications of SARS-CoV-2 in wastewater are described in [Hewitt et al 2022](https://www.sciencedirect.com/science/article/pii/S0043135421012264).


Wastewater sites are selected based on several factors including population and geographic coverage. New sites may be added over time and/or sampling may reduce in frequency or cease for other sites. Typically, samples are collected twice per week from larger wastewater catchments and once a week from smaller towns and communities. This is also subject to change.

Most samples are collected by an autosampler, which collects a small volume of wastewater at regular intervals over the course of a 25-hour period. When composite samplers are not available, 'grab' samples are collected. These range from a sample being taken at a single point in time, to 3 samples taken over 30 minutes, to multiple samples collected over a day. Grab samples represent only the composition of the sources at that time of collection and may not be as representative as a 24-hour composite sample. More variation may be expected with grab samples, samples collected from smaller catchments (an individual case can have a disproportionately large effect on overall viral level in small catchments) and from sites that are only sampled once per week.

The catchment polygons are not included. They are the intellectual property of the individual regional and city councils that operate the treatment plants that we sample from. Some are available publicly, otherwise if you are interested in obtaining specific GIS files for a site, we suggest contacting the relevant council.

## Wastewater Data

The wastewater data shows the SARS-CoV-2 genome copies per litre measured from either an autosampler/grab sample (see lab analysis and methodology for more details). To preserve anonymity of sites with small populations we have excluded these from the site-specific data. These are however still included in the aggregated regional and national wastewater data.

### Site Aggregation

For each sample location if more than one sample is taken this is averaged to get the average copies per person per day for the site that week. This is then normalised using population and wastewater flow.

### Regional Aggregation

For the regional aggregated data the averaged site data that has been normalised is aggregated using a weighted average to ensure smaller catchments are not over-represented and large catchments are not under represented. A 7-day average is then reported for Monday-Sunday.

### National Aggregation

The averaged normalised site data is aggregated and for a week and weighted by the total population covered by the sites tested this week. This ensures each week is taking into consideration the differences in population covered week to week. A 7-day average is then reported for Monday-Sunday.

## Clinical Case Data


Case numbers are calculated by summing up all the new cases reported to the Ministry of Health for that week. Cases are reported on a per-day basis because wastewater samples are generally representative of the viral load in the catchment for the preceding 24-hrs. The report date is aligned with what the Ministry of Health publishes on their website. The average number of new COVID-19 cases reported per day via are collected through NCTS or [EpiSurv](https://surv.esr.cri.nz/episurv/index.php), when report date is not available the first non null value from the fields onset date, lab sample date, lab confirmed detection date or earliest date.

## Data Dictionary

### National Data

**cases_national.csv**

-   week_end_date: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   case_7d_avg: average number of new COVID-19 cases reported per day using reported date if not available first non-null value for onset date, lab sample date, lab confirm detection or earliest date.

**ww_national.csv**

-   week_end_date: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   national_population: the sum of catchment populations covered by testing that week.

-   copies_per_person_per_day: An average of the SARS-CoV-2 genome copies per person per day. Raw SARS-CoV-2 genome copies results are normalised by ctchment for population covered by testing and normalised for wastewater flow per day. Calculated as an average of results from the previous 7 days.

### Regional Data

**cases_regional.csv**

-   week_end_date: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   Region: region name.

-   case_7d_avg: average number of new COVID-19 cases reported per day using reported date if not available first non-null value for onset date, lab sample date, lab confirm detection or earliest date.

**ww_regional.csv**

-   week_end_date: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   Region: region name

-   copies_per_person_per_day: An average of the SARS-CoV-2 genome copies per person per day. Raw SARS-CoV-2 genome copies results are normalised by catchment for population covered by testing and normalised for wastewater flow per day. Calculated as an average of results from the previous 7 days.

-   n_site: number of sites within the region contributing to each week's data.

### Site Data

**cases_site.csv**

-   week_end_date: end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   SampleLocation: wastewater testing site name ("AU_Rosedale").

-   copies_per_person_per_day: An average of the SARS-CoV-2 genome copies per person per day. Raw SARS-CoV-2 genome copies results are normalised by ctchment for population covered by testing and normalised for wastewater flow per day. Calculated as an average of results from the previous 7 days.

***Note:*** Where meshblocks straddle a watershed between two catchments, the case will be reported for both catchments. To aggregate to higher geographies, please use the *cases_regional.csv* or *cases_national.csv* files to avoid double counting.

**ww_site.csv**

-   end of week date for week covered between Monday-Sunday (YYYY-MM-DD).

-   SampleLocation: wastewater testing site name ("AU_Rosedale").

-   case_7d_avg: An average of the SARS-CoV-2 genome copies per person per day. Raw SARS-CoV-2 genome copies results are normalised by ctchment for population covered by testing and normalised for wastewater flow per day. Calculated as an average of results from the previous 7 days.

**sites.csv**

-   SampleLocation: wastewater testing site name ("AU_Rosedale").

-   DisplayName: display name used for reporting ("Rosedale").

-   SampleType: sampling method used; autosampler or grab.

-   Latitude: The latitude of the sampling location, typically a wastewater treatment plant.

-   Longitude: The longitude of the sampling location.

-   Population: The estimated population covered by the wastewater catchment area.

-   Region: region name site is located in.

-   shp_label: a unique identifier for the catchment polygons.


**variants_last_two_weeks.csv**

- variant: variant name

- DisplayName: site display name used on the variants chart

- detected: boolean (true or false) to indicate whether the variant was detected

***Note:*** Variant analysis for wastewater is an emergent field. Due to the increasing complexity of variants in the population, each at relatively low levels, the current approach for sequencing wastewater samples is no longer precise enough to report as percentages for each variant at the sentinel site level. Instead, the presence of each lineage is reported. 

ESR are actively testing and developing methods to address the current uncertainty and increase the resolution at which variants can be identified in wastewater.

For further guidance, please refer to the 'Estimated variant prevalence' notes on the [wastewater dashboard](https://esr-cri.shinyapps.io/wastewater/#page=About).


### Raw Wastewater Data

**ww_data_all.csv**

-   SampleLocation: wastewater testing site name ("AU_Rosedale").

-   sars_gcl: The amount of SARS-CoV-2 genome copies per litre of wastewater.

-   Result: Either "Detected" if SARS-CoV-2 was identified in the wastewater sample or "Not detected".

-   copies_per_person_per_day: An average of the SARS-CoV-2 genome copies per person per day. Raw SARS-CoV-2 genome copies results are normalised by ctchment for population covered by testing and normalised for wastewater flow per day. Calculated as an average of results from the previous 7 days.

## Laboratory Methodology

Samples are sent from each wastewater treatment plant to ESR. Processing first involves separating the solids from liquid by centrifugation, followed by eluting the virus from the solids. The virus from the solids is then combined with that in the liquid phase and concentrated to a small volume by polyethylene glycol (PEG) precipitation. The viral RNA is extracted using a commercial viral nucleic acid extraction kit. The presence of SARS-CoV-2 RNA in the sample is then determined using RT-qPCR (reverse transcription-quantitative polymerase chain reaction) with the N gene of the SARS-C-2 viral genome. The presence of SARS-CoV-2 is considered detected when any of the RT-qPCR replicates are positive. A result of not detected means that SARS-CoV-2 RNA is either absent from the sample, or at a level too low to be detected.

When SARS-CoV-2 RNA is detected by RT-qPCR, the concentration in the sample is calculated and converted from genome copy per reaction into genome copies per litre of wastewater (i.e., raw data). The unit conversion considers the initial sample volume, final volume of the concentrate used for RNA extraction, final volume of the eluted RNA, and amount of RNA used in the RT-qPCR template. Low amounts of SARS-CoV-2 RNA in a sample may not be able to be accurately quantified and are recorded as 500 genome copies/L.


## Citation

If you would like to use this data, please cite: COVID-19 Data Repository by the Institute of Environmental Science and Research", and the url: <https://github.com/ESR-NZ/covid_in_wastewater>

For academic publications, cite the following paper:

> Hewitt, Joanne, et al. "Sensitivity of wastewater-based epidemiology for detection of SARS-CoV-2 RNA in a low prevalence setting." Water research 211 (2022): 118032. <https://doi.org/10.1021/acsestwater.1c00434>

## Acknowledgements

This work represents the combined efforts of many individuals and organisations.

We continue to be indebted to the teams across the country who are collecting the wastewater and associated metadata that underpins this work.

ESR acknowledges the support of councils and wastewater providers across New Zealand who provide us with samples and staff in the public health services in New Zealand who provide us with data from their regions.

## Terms of Use:

1.  This dataset is owned by the Institute of Environmental Science and Research Limited and licensed for reuse under the [Creative Commons Attribution 4.0 International licence](https://creativecommons.org/licenses/by/4.0/). This license means that you are free to copy, distribute and adapt the material, as long as you attribute it to the Institute of Environmental Science and Research Limited and abide by the other license terms. This license does not apply to any logos and trade marks on this website – these specific elements may not be reused without the Institute of Environmental Science and Research Limited's prior written consent.
2.  If you wish to use the data, you must attribute it as the "COVID-19 Data Repository by the Institute of Environmental Science and Research", and the url: <https://github.com/ESR-NZ/covid_in_wastewater>
3.  You may use our application programming interface ("API") to facilitate access to the dataset, whether through a separate website or through another type of software application.
4.  You may not represent or imply that the Institute of Environmental Science and Research Limited has approved or endorsed the manner or purpose of your use or reproduction of the dataset.
5.  The Institute of Environmental Science and Research Limited reserves the right at any time in its sole discretion to modify or discontinue (temporarily or permanently) this website, the dataset, and any means of accessing the dataset, with or without prior notice to you.

## Disclaimer:

Data is shared solely for the benefit of the Ministry of Health (MoH), Public Health Service Providers and other Third Party Beneficiaries as defined in the Contract between ESR and the MoH. ESR does not accept any legal liability or responsibility for use of information contained in this repository by any other person or organisation.

## About ESR

The Institute of Environmental Science and Research (ESR) is a crown research institute in Aotearoa. ESR provides science services and research capability across a number of science disciplines including; public Health, Forensics, Water and the Environment, Genomics and Social Science.
