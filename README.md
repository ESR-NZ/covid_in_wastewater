## New Zealand SARS-CoV-2 testing in Wastewater

This git repo contains the datasets used to support ESR's [SARS-CoV-2 in wastewater](https://www.esr.cri.nz/our-expertise/covid-19-response/wastewater-testing-results/) testing programme.

Files are updated weekly.

It consists of the following files:

### cases_national.csv

The weekly average of new COVID-19 cases reported per day.

**week_end_date** = the last date of the week covered (Monday-Sunday)

**case_7d_avg** = the average number of new COVID-19 cases reported per day via NCTS or Episurv, using the ReportDate where this is available and where not falling back on the first non null value from the fields OnsetDt, LabSampleDate, LabConfDt or EarliestDate

### cases_regional.csv

The weekly average of new COVID-19 cases reported per day by region.

**week_end_date** = the last date of the week covered (Monday-Sunday)

**Region** = This is based on a lookup table between the case's meshblock and a region

**case_7d_avg** = the average number of new COVID-19 cases reported per day via NCTS or Episurv, using the ReportDate where this is available and where not falling back on the first non null value from the fields OnsetDt, LabSampleDate, LabConfDt or EarliestDate

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

## sars_cov2_wastewater_aotearoa.xslx

An excel file which combines each of the .csv files as different sheets in one file.

&nbsp;

##### For more information about the wastewater testing programme and the methodology of metric calculations, refer to the [covid insights](https://www.esr.cri.nz/covid-insights) page. 
