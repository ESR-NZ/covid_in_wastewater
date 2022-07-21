# New Zealand SARS-CoV-2 testing in Wastewater

This git repo contains the datasets used to support ESR's [SARS-CoV-2 in wastewater](https://www.esr.cri.nz/our-expertise/covid-19-response/wastewater-testing-results/) testing programme.

### **Provided by Institute of Environmental Science and Research (ESR)**

<https://www.esr.cri.nz/>

Funding for the Dashboard and Data Repository was provided by the Ministry of Health.

<https://www.health.govt.nz/>

### Acknowledgements

ESR acknowledges the support of wastewater providers across New Zealand who provide us with samples and staff in the public health services in New Zealand who provide us with data from their regions.

### Terms of Use:

1.  This dataset is owned by the Institute of Environmental Science and Research Limited and licensed for reuse under the [Creative Commons Attribution 4.0 International licence](https://creativecommons.org/licenses/by/4.0/). This license means that you are free to copy, distribute and adapt the material, as long as you attribute it to the Institute of Environmental Science and Research Limited and abide by the other license terms. This license does not apply to any logos and trade marks on this website – these specific elements may not be reused without the Institute of Environmental Science and Research Limited's prior written consent.
2.  If you wish to use the data, you must attribute it as the "COVID-19 Data Repository by the Institute of Environmental Science and Research", and the url: <https://github.com/ESR-NZ/covid_in_wastewater>
3.  You may use our application programming interface ("API") to facilitate access to the dataset, whether through a separate website or through another type of software application.
4.  You may not represent or imply that the Institute of Environmental Science and Research Limited has approved or endorsed the manner or purpose of your use or reproduction of the dataset.
5.  The Institute of Environmental Science and Research Limited reserves the right at any time in its sole discretion to modify or discontinue (temporarily or permanently) this website, the dataset, and any means of accessing the dataset, with or without prior notice to you.

### Disclaimer:

Data is shared solely for the benefit of the Ministry of Health (MoH), Public Health Service Providers and other Third Party Beneficiaries as defined in the Contract between ESR and the MoH. ESR does not accept any legal liability or responsibility for use of information contained in this repository by any other person or organisation.

## Contents:

The the following files are provided:

### cases_national.csv

The weekly average of new COVID-19 cases reported per day.

**week_end_date** = the last date of the week covered (Monday-Sunday)

**case_7d_avg** = the average number of new COVID-19 cases reported per day via NCTS or Episurv, using the ReportDate where this is available and where not falling back on the first non null value from the fields OnsetDt, LabSampleDate, LabConfDt or EarliestDate.

### cases_regional.csv

The weekly average of new COVID-19 cases reported per day by region.

**week_end_date** = the last date of the week covered (Monday-Sunday)

**Region** = This is based on a lookup table between the case's meshblock and a region

**case_7d_avg** = the average number of new COVID-19 cases reported per day via NCTS or Episurv, using the ReportDate where this is available and where not falling back on the first non null value from the fields OnsetDt, LabSampleDate, LabConfDt or EarliestDate.

### cases_site.csv

The weekly average of new COVID-19 cases reported by catchment.

**week_end_date** = the last date of the week covered (Monday-Sunday)

**SampeLocation** = An identifier for a wastewater testing site. Cases are allocated a catchment based on a lookup table between the case's meshblock.

**case_7d_avg** = the average number of new COVID-19 cases reported per day via NCTS or Episurv, using the ReportDate where this is available and where not falling back on the first non null value from the fields OnsetDt, LabSampleDate, LabConfDt or EarliestDate

*Note* - Where meshblocks straddle a watershed between two catchments, the case will be reported for both catchments. To aggregate to higher geographies, please use the cases_regional or cases_national files to avoid double counting.

### sites.csv

Information about wastewater testing locations.

**SampleLocation** = A unique identifier for each wastewater testing site.

**DisplayName** = The site name used in reporting.

**SampleType** = Whether an autosampler or a grab sample is used - see the About page on the dashboard for more information.

**Latitude & Longitude** = The geographic coordinates of the sampling location, typically a wastewater treatment works.

**Population** = The estimated population covered by the wastewater catchment area.

**Region** = The administrative region of New Zealand.

**shp_label** = A unique identifier for the catchment polygons.

### ww_data_all.csv

This table contains individual test results from a site for a sample taken on a particular date. This data is not currently displayed on the wastewater dashboard. Instead it is aggregated together across all results from a site each week and published in the ww_national, ww_regional and ww_site tables.

**SampleLocation** = Site code.

**sars_gcl** = The number of SARS-CoV-2 genome copies per litre of wastewater.

**Collected** = The date of collection for the sample.

**Result** = Either "Detected" if SARS-CoV-2 was identified in the wastewater sample, or "Not detected".

**copies_per_day_per_person** = The estimated number of SARS-CoV-2 genome copies passing through a wastewater sampling site per day per person living within the catchment.

### ww_national.csv

**week_end_date** = The last day of the 7 day reporting period (Monday-Sunday).

**national_population** = The sum of catchment populations covered in each week's report.

**copies_per_day_per_person** = The national number of SARS-CoV-2 genome per person per day copies taking in to account all sites reporting within the 7 day period.

### ww_regional.csv

**week_end_date** = The last day of the 7 day reporting period (Monday-Sunday).

**Region** = The region name.

**copies_per_day_per_person** = The number of SARS-CoV-2 genome copies per person per day taking in to account all sites in the region reporting within the 7 day period.

**n_sites** = The number of sites within the region contributing to each week's data.

### ww_site.csv

**week_end_date** = The last day of the 7 day reporting period (Monday-Sunday).

**SampleLocation** = An identifier for a wastewater testing site.

**copies_per_day_per_person** = The number of SARS-CoV-2 genome copies per person per day. Where multiple samples were taken from a site during a week, this value is averaged.

### sars_cov2_wastewater_aotearoa.xslx

An excel file which combines each of the .csv files as different sheets in one file.

 

For more information about the wastewater testing programme and the methodology of metric calculations, refer to our [covid insights](https://www.esr.cri.nz/covid-insights) page.
