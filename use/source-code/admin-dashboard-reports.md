# Admin Dashboard Reports

As part of Sunbird ED we have the following list of reports available in the "Admin Dashboard Page" For Report Admin and for the Report Viewer Roles. \
\
Below is the list of reports that Report Admin and Report Viewer users can see in the \
Admin Dashboard Portal&#x20;

* ETB Creation Status Report
* Live ETB QR Code-Content Linkage Status
* Course Adoption Report v2

### ETB Level Report

In this report, we are showning all the textbooks created under that tenant and their consumption in TWO Reports

* ETB Creation Status Report
* Live ETB QR Code-Content Linkage Status\


**ETB Creation Status Report:** This report provides details about the creation status of all textbooks. Note that the numbers shown in the graphs are absolute numbers and not percentages.

This report helps administrators to track the ETB creation process, identify textbooks that are incomplete and take actions to complete the process.

**Live ETB QR Code-Content Linkage Status:** This report provides the details of QR codes present in the live textbooks that have content linked and content not linked to them. Detailed data table also provides specific QR codes that do not have linked content along with the total number of scans.

QR codes without any content linked to them result in bad user experience. This report helps in identifying such QR codes and take immediate action by linking content to them.\


More Detailes of this report are available in this Confluance Page: [https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/1044643843/ETB+Creation+report+and+QR+Code+Exception+report](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/1044643843/ETB+Creation+report+and+QR+Code+Exception+report)\
\
\
To Run the Report:\
&#x20;Deploy/Lern/LernAnalyticsReplayJobs\
&#x20;job\_type: run-job \
&#x20;job\_id: etb-metrics\
Before running the above jobs we need to make sure there is data available in these data sets (content-model-snapshot, summary-rollup-syncts, & telemetry-rollup-syncts)

The script of this report is available in this [link](https://github.com/Sunbird-Lern/data-products/tree/release-5.3.1)

### Course Adoption Report v2

&#x20;   In this report, we are showing all the courses created under that tenant and their consumption by batch-wise State and District.

#### To Run the Report:&#x20;

Deploy/DataPipeline/Runreport

JOB id: course\_adoption\_by\_batch \
&#x20;            course\_adoption\_table\_new \
&#x20;            course\_adoption\_report\_plays\_and\_time\_spent

Before running the above three jobs we need to make sure there is data available in these data sets (collection-summary-snapshots & summary-rollup-syncs)

#### **DataSource( In Druid)**

We have to configure the datasource in Druid to index all the required fields for the sourcing admin reports. Find the below details of the Druid datasource.

#### **DataSource -**&#x20;

This report is dependent on the following data sources&#x20;

* collection-summary-snapshots&#x20;
* summary-rollup-syncts\
  \
  **{Screenshot needs to be added}**\


#### **Configuration**

For "**Course Adoption**" we have to configure the report using the "ReportConfigure" API. The \`reportId\` is the key to identify the report is configured or not

`"reportId": "`course\_adoption\_by\_batch`", "`course\_adoption\_table\_new`", "`course\_adoption\_report\_plays\_and\_time\_spent`"`

API -

```
{{host}}api/data/v1/report/jobs/course_adoption_by_batch
```

**Request Body**

{% code fullWidth="false" %}
```
{
  "createdOn": 1624433765307,
  "updatedOn": 1627728823592,
  "reportId": "course_adoption_by_batch",
  "config": {
    "streamQuery": true,
    "reportConfig": {
      "id": "course_adoption_by_batch",
      "mergeConfig": {
        "postContainer": "reports",
        "container": "reports",
        "basePath": "/mount/data/analytics/tmp",
        "reportPath": "course_adoption_by_batch.csv",
        "dateFieldRequired": false,
        "rollup": 0
      },
      "labels": {
        "batch_start_date": "Batch Start Date",
        "collection_id": "Collection id",
        "batch_end_date": "Batch End Date",
        "total_content_plays_on_app": "Total Completion",
        "total_content_plays_on_desktop": "Total Certificates Issued",
        "legend": "Total Enrolments",
        "channel_for_slug": "Content Published by",
        "SUM(total_certificates_issued)": "total_content_plays_on_desktop",
        "total_content_plays_on_portal": "Total Enrolments",
        "batch_name": "Batch Name",
        "batch_id": "Batch id",
        "collection_name": "Collection Name",
        "Content Published by": "Published by"
      },
      "dateRange": {
        "staticInterval": "LastDay",
        "granularity": "latest_index",
        "intervalSlider": 0
      },
      "metrics": [
        {
          "metric": "total_content_plays_on_portal",
          "label": "total_content_plays_on_portal",
          "druidQuery": {
            "dataSource": "collection-summary-snapshot",
            "limitSpec": {
              "type": "default",
              "limit": 50000,
              "columns": [
                {
                  "dimension": "SUM(total_enrolment)",
                  "direction": "descending"
                }
              ]
            },
            "granularity": "latest_index",
            "dimensions": [
              {
                "type": "extraction",
                "extractionFn": [
                  {
                    "type": "registeredLookup",
                    "retainMissingValue": true,
                    "fn": "channelSlugLookup"
                  }
                ],
                "fieldName": "created_for",
                "aliasName": "Content Published by"
              },
              {
                "fieldName": "collection_name",
                "aliasName": "Collection Name"
              },
              {
                "fieldName": "collection_id",
                "aliasName": "Collection id"
              },
              {
                "fieldName": "batch_name",
                "aliasName": "Batch Name"
              },
              {
                "fieldName": "batch_id",
                "aliasName": "Batch id"
              },
              {
                "fieldName": "batch_start_date",
                "aliasName": "Batch Start Date"
              },
              {
                "fieldName": "batch_end_date",
                "aliasName": "Batch End Date"
              }
            ],
            "aggregations": [
              {
                "fieldName": "total_enrolment",
                "type": "longSum",
                "name": "total_content_plays_on_portal"
              }
            ],
            "postAggregations": [],
            "queryType": "groupBy"
          }
        },
        {
          "metric": "total_content_plays_on_app",
          "label": "Total Completion",
          "druidQuery": {
            "dataSource": "collection-summary-snapshot",
            "limitSpec": {
              "type": "default",
              "limit": 50000,
              "columns": [
                {
                  "dimension": "SUM(total_completion)",
                  "direction": "descending"
                }
              ]
            },
            "granularity": "latest_index",
            "dimensions": [
              {
                "type": "extraction",
                "extractionFn": [
                  {
                    "type": "registeredLookup",
                    "retainMissingValue": true,
                    "fn": "channelSlugLookup"
                  }
                ],
                "fieldName": "created_for",
                "aliasName": "Content Published by"
              },
              {
                "fieldName": "collection_name",
                "aliasName": "Collection Name"
              },
              {
                "fieldName": "collection_id",
                "aliasName": "Collection id"
              },
              {
                "fieldName": "batch_name",
                "aliasName": "Batch Name"
              },
              {
                "fieldName": "batch_id",
                "aliasName": "Batch id"
              },
              {
                "fieldName": "batch_start_date",
                "aliasName": "Batch Start Date"
              },
              {
                "fieldName": "batch_end_date",
                "aliasName": "Batch End Date"
              }
            ],
            "aggregations": [
              {
                "fieldName": "total_completion",
                "type": "longSum",
                "name": "total_content_plays_on_app"
              }
            ],
            "postAggregations": [],
            "queryType": "groupBy"
          }
        },
        {
          "metric": "total_content_plays_on_desktop",
          "label": "Total Certificates Issued",
          "druidQuery": {
            "dataSource": "collection-summary-snapshot",
            "limitSpec": {
              "type": "default",
              "limit": 50000,
              "columns": [
                {
                  "dimension": "SUM(total_certificates_issued)",
                  "direction": "descending"
                }
              ]
            },
            "granularity": "latest_index",
            "dimensions": [
              {
                "type": "extraction",
                "extractionFn": [
                  {
                    "type": "registeredLookup",
                    "retainMissingValue": true,
                    "fn": "channelSlugLookup"
                  }
                ],
                "fieldName": "created_for",
                "aliasName": "Content Published by"
              },
              {
                "fieldName": "collection_name",
                "aliasName": "Collection Name"
              },
              {
                "fieldName": "collection_id",
                "aliasName": "Collection id"
              },
              {
                "fieldName": "batch_name",
                "aliasName": "Batch Name"
              },
              {
                "fieldName": "batch_id",
                "aliasName": "Batch id"
              },
              {
                "fieldName": "batch_start_date",
                "aliasName": "Batch Start Date"
              },
              {
                "fieldName": "batch_end_date",
                "aliasName": "Batch End Date"
              }
            ],
            "aggregations": [
              {
                "fieldName": "total_certificates_issued",
                "type": "longSum",
                "name": "total_content_plays_on_desktop"
              }
            ],
            "postAggregations": [],
            "queryType": "groupBy"
          }
        }
      ],
      "output": [
        {
          "type": "csv",
          "metrics": [
            "total_content_plays_on_portal",
            "total_content_plays_on_app",
            "total_content_plays_on_desktop"
          ],
          "dims": [
            "date",
            "Content Published by"
          ],
          "fileParameters": [
            "id",
            "dims"
          ]
        }
      ],
      "queryType": "groupBy"
    },
    "container": "reports",
    "store": "oci",
    "key": "hawk-eye/"
  },
  "requestedBy": "User1",
  "reportDescription": "Course Adoption Report",
  "submittedOn": 1624433765307,
  "status": "ACTIVE",
  "status_msg": "REPORT SUCCESSFULLY ACTIVATED",
  "reportSchedule": "DAILY"
}
```
{% endcode %}



```
{
        "createdOn": 1621514149909,
        "updatedOn": 1627729035091,
        "reportId": "course_adoption_table_new",
        "config": {
            "streamQuery": true,
            "reportConfig": {
                "id": "course_adoption_table_new",
                "mergeConfig": {
                    "postContainer": "reports",
                    "container": "reports",
                    "basePath": "/mount/data/analytics/tmp",
                    "reportPath": "course_adoption_table_new.csv",
                    "dateFieldRequired": false,
                    "rollup": 0
                },
                "labels": {
                    "batch_start_date": "Batch Start Date",
                    "state": "User State",
                    "collection_id": "Collection id",
                    "batch_end_date": "Batch End Date",
                    "total_content_plays_on_app": "Total Completions",
                    "total_content_plays_on_desktop": "Total Certificates Issued",
                    "legend": "Total Enrolments",
                    "channel_for_slug": "Content Published by",
                    "SUM(total_certificates_issued)": "total_content_plays_on_desktop",
                    "total_content_plays_on_portal": "Total Enrolments",
                    "user_state": "state",
                    "batch_name": "Batch Name",
                    "user_district": "User District",
                    "batch_id": "Batch id",
                    "collection_name": "Collection Name",
                    "Content Published by": "Published by",
                    "has_certificate": "Has Certificate"
                },
                "dateRange": {
                    "staticInterval": "LastDay",
                    "granularity": "latest_index",
                    "intervalSlider": 0
                },
                "metrics": [
                    {
                        "metric": "total_content_plays_on_portal",
                        "label": "total_content_plays_on_portal",
                        "druidQuery": {
                            "dataSource": "collection-summary-snapshot",
                            "limitSpec": {
                                "type": "default",
                                "limit": 1000,
                                "columns": [
                                    {
                                        "dimension": "SUM(total_enrolment)",
                                        "direction": "descending"
                                    }
                                ]
                            },
                            "filters": [
                                {
                                    "type": "equals",
                                    "dimension": "content_status",
                                    "value": "Live"
                                }
                            ],
                            "granularity": "latest_index",
                            "dimensions": [
                                {
                                    "type": "extraction",
                                    "extractionFn": [
                                        {
                                            "type": "registeredLookup",
                                            "retainMissingValue": true,
                                            "fn": "channelSlugLookup"
                                        }
                                    ],
                                    "fieldName": "created_for",
                                    "aliasName": "Content Published by"
                                },
                                {
                                    "fieldName": "collection_id",
                                    "aliasName": "Collection id"
                                },
                                {
                                    "fieldName": "collection_name",
                                    "aliasName": "Collection Name"
                                },
                                {
                                    "fieldName": "batch_id",
                                    "aliasName": "Batch id"
                                },
                                {
                                    "fieldName": "batch_name",
                                    "aliasName": "Batch Name"
                                },
                                {
                                    "fieldName": "batch_start_date",
                                    "aliasName": "Batch Start Date"
                                },
                                {
                                    "fieldName": "batch_end_date",
                                    "aliasName": "Batch End Date"
                                },
                                {
                                    "fieldName": "has_certificate",
                                    "aliasName": "Has Certificate"
                                },
                                {
                                    "fieldName": "user_state",
                                    "aliasName": "state"
                                },
                                {
                                    "fieldName": "user_district",
                                    "aliasName": "User District"
                                }
                            ],
                            "aggregations": [
                                {
                                    "fieldName": "total_enrolment",
                                    "type": "longSum",
                                    "name": "total_content_plays_on_portal"
                                }
                            ],
                            "postAggregations": [],
                            "queryType": "groupBy"
                        }
                    },
                    {
                        "metric": "total_content_plays_on_app",
                        "label": "Total Completions",
                        "druidQuery": {
                            "dataSource": "collection-summary-snapshot",
                            "limitSpec": {
                                "type": "default",
                                "limit": 1000,
                                "columns": [
                                    {
                                        "dimension": "SUM(total_completion)",
                                        "direction": "descending"
                                    }
                                ]
                            },
                            "filters": [
                                {
                                    "type": "equals",
                                    "dimension": "content_status",
                                    "value": "Live"
                                }
                            ],
                            "granularity": "latest_index",
                            "dimensions": [
                                {
                                    "type": "extraction",
                                    "extractionFn": [
                                        {
                                            "type": "registeredLookup",
                                            "retainMissingValue": true,
                                            "fn": "channelSlugLookup"
                                        }
                                    ],
                                    "fieldName": "created_for",
                                    "aliasName": "Content Published by"
                                },
                                {
                                    "fieldName": "collection_id",
                                    "aliasName": "Collection id"
                                },
                                {
                                    "fieldName": "collection_name",
                                    "aliasName": "Collection Name"
                                },
                                {
                                    "fieldName": "batch_id",
                                    "aliasName": "Batch id"
                                },
                                {
                                    "fieldName": "batch_name",
                                    "aliasName": "Batch Name"
                                },
                                {
                                    "fieldName": "batch_start_date",
                                    "aliasName": "Batch Start Date"
                                },
                                {
                                    "fieldName": "batch_end_date",
                                    "aliasName": "Batch End Date"
                                },
                                {
                                    "fieldName": "has_certificate",
                                    "aliasName": "Has Certificate"
                                },
                                {
                                    "fieldName": "user_state",
                                    "aliasName": "state"
                                },
                                {
                                    "fieldName": "user_district",
                                    "aliasName": "User District"
                                }
                            ],
                            "aggregations": [
                                {
                                    "fieldName": "total_completion",
                                    "type": "longSum",
                                    "name": "total_content_plays_on_app"
                                }
                            ],
                            "postAggregations": [],
                            "queryType": "groupBy"
                        }
                    },
                    {
                        "metric": "total_content_plays_on_desktop",
                        "label": "Total Certificates Issued",
                        "druidQuery": {
                            "dataSource": "collection-summary-snapshot",
                            "limitSpec": {
                                "type": "default",
                                "limit": 1000,
                                "columns": [
                                    {
                                        "dimension": "SUM(total_certificates_issued)",
                                        "direction": "descending"
                                    }
                                ]
                            },
                            "filters": [
                                {
                                    "type": "equals",
                                    "dimension": "content_status",
                                    "value": "Live"
                                }
                            ],
                            "granularity": "latest_index",
                            "dimensions": [
                                {
                                    "type": "extraction",
                                    "extractionFn": [
                                        {
                                            "type": "registeredLookup",
                                            "retainMissingValue": true,
                                            "fn": "channelSlugLookup"
                                        }
                                    ],
                                    "fieldName": "created_for",
                                    "aliasName": "Content Published by"
                                },
                                {
                                    "fieldName": "collection_id",
                                    "aliasName": "Collection id"
                                },
                                {
                                    "fieldName": "collection_name",
                                    "aliasName": "Collection Name"
                                },
                                {
                                    "fieldName": "batch_id",
                                    "aliasName": "Batch id"
                                },
                                {
                                    "fieldName": "batch_name",
                                    "aliasName": "Batch Name"
                                },
                                {
                                    "fieldName": "batch_start_date",
                                    "aliasName": "Batch Start Date"
                                },
                                {
                                    "fieldName": "batch_end_date",
                                    "aliasName": "Batch End Date"
                                },
                                {
                                    "fieldName": "has_certificate",
                                    "aliasName": "Has Certificate"
                                },
                                {
                                    "fieldName": "user_state",
                                    "aliasName": "state"
                                },
                                {
                                    "fieldName": "user_district",
                                    "aliasName": "User District"
                                }
                            ],
                            "aggregations": [
                                {
                                    "fieldName": "total_certificates_issued",
                                    "type": "longSum",
                                    "name": "total_content_plays_on_desktop"
                                }
                            ],
                            "postAggregations": [],
                            "queryType": "groupBy"
                        }
                    }
                ],
                "output": [
                    {
                        "type": "csv",
                        "metrics": [
                            "total_content_plays_on_portal",
                            "total_content_plays_on_app",
                            "total_content_plays_on_desktop"
                        ],
                        "dims": [
                            "date",
                            "Content Published by"
                        ],
                        "fileParameters": [
                            "id",
                            "dims"
                        ]
                    }
                ],
                "queryType": "groupBy"
            },
            "container": "reports",
            "store": "oci",
            "key": "hawk-eye/"
        },
        "createdBy": "User1",
        "description": "Course Adoption Report",
        "submittedOn": 1621514149909,
        "status": "ACTIVE",
        "status_msg": "REPORT SUCCESSFULLY ACTIVATED",
        "reportSchedule": "DAILY"
    }
```







```
{
    "id": "ekstep.analytics.report.get",
    "params": {
        "client_key": null,
        "resmsgid": "50501709-3e75-4fd6-8c97-4fa709fc2616",
        "status": "successful"
    },
    "responseCode": "OK",
    "result": {
        "config": {
            "container": "reports",
            "key": "hawk-eye/",
            "reportConfig": {
                "dateRange": {
                    "granularity": "all",
                    "interval": {
                        "endDate": "2101-01-01",
                        "startDate": "1901-01-01"
                    },
                    "intervalSlider": 0
                },
                "id": "course_adoption_report_plays_and_time_spent",
                "labels": {
                    "collection_for_slug": "state",
                    "collection_name": "Course Name",
                    "data": "Date",
                    "legend": "Total Plays",
                    "object_rollup_l1": "Course id",
                    "state": "State",
                    "total_content_plays_on_app": "Total Time Spent (Hrs)",
                    "total_content_plays_on_portal": "Total Plays",
                    "total_time_spent_hours": "total_content_plays_on_app"
                },
                "mergeConfig": {
                    "basePath": "/mount/data/analytics/tmp",
                    "container": "reports",
                    "dateFieldRequired": false,
                    "postContainer": "reports",
                    "reportPath": "course_adoption_report_plays_and_time_spent.csv",
                    "rollup": 0
                },
                "metrics": [
                    {
                        "druidQuery": {
                            "aggregations": [
                                {
                                    "fieldName": "total_count",
                                    "name": "total_content_plays_on_portal",
                                    "type": "longSum"
                                }
                            ],
                            "dataSource": "summary-rollup-syncts",
                            "dimensions": [
                                {
                                    "aliasName": "state",
                                    "extractionFn": [
                                        {
                                            "fn": "channelSlugLookup",
                                            "retainMissingValue": true,
                                            "type": "registeredLookup"
                                        }
                                    ],
                                    "fieldName": "collection_created_for",
                                    "type": "extraction"
                                },
                                {
                                    "aliasName": "Course id",
                                    "fieldName": "object_rollup_l1"
                                },
                                {
                                    "aliasName": "Course Name",
                                    "fieldName": "collection_name"
                                }
                            ],
                            "filters": [
                                {
                                    "dimension": "collection_type",
                                    "type": "equals",
                                    "value": "Course"
                                },
                                {
                                    "dimension": "dimensions_type",
                                    "type": "equals",
                                    "value": "content"
                                },
                                {
                                    "dimension": "dimensions_mode",
                                    "type": "equals",
                                    "value": "play"
                                }
                            ],
                            "granularity": "all",
                            "limitSpec": {
                                "columns": [
                                    {
                                        "dimension": "SUM(total_count)",
                                        "direction": "descending"
                                    }
                                ],
                                "limit": 50000,
                                "type": "default"
                            },
                            "postAggregations": [
                            ],
                            "queryType": "groupBy"
                        },
                        "label": "total_content_plays_on_portal",
                        "metric": "total_content_plays_on_portal"
                    },
                    {
                        "druidQuery": {
                            "aggregations": [
                                {
                                    "fieldName": "total_time_spent",
                                    "name": "sum__total_time_spent",
                                    "type": "doubleSum"
                                }
                            ],
                            "dataSource": "summary-rollup-syncts",
                            "dimensions": [
                                {
                                    "aliasName": "state",
                                    "extractionFn": [
                                        {
                                            "fn": "channelSlugLookup",
                                            "retainMissingValue": true,
                                            "type": "registeredLookup"
                                        }
                                    ],
                                    "fieldName": "collection_created_for",
                                    "type": "extraction"
                                },
                                {
                                    "aliasName": "Course id",
                                    "fieldName": "object_rollup_l1"
                                },
                                {
                                    "aliasName": "Course Name",
                                    "fieldName": "collection_name"
                                }
                            ],
                            "filters": [
                                {
                                    "dimension": "collection_type",
                                    "type": "equals",
                                    "value": "Course"
                                },
                                {
                                    "dimension": "dimensions_type",
                                    "type": "equals",
                                    "value": "content"
                                },
                                {
                                    "dimension": "dimensions_mode",
                                    "type": "equals",
                                    "value": "play"
                                }
                            ],
                            "granularity": "all",
                            "limitSpec": {
                                "columns": [
                                    {
                                        "dimension": "total_time_spent_hours",
                                        "direction": "descending"
                                    }
                                ],
                                "limit": 50000,
                                "type": "default"
                            },
                            "postAggregation": [
                                {
                                    "fields": {
                                        "leftField": "sum__total_time_spent",
                                        "rightField": 3600,
                                        "rightFieldType": "constant"
                                    },
                                    "fn": "/",
                                    "name": "total_content_plays_on_app",
                                    "type": "arithmetic"
                                }
                            ],
                            "queryType": "groupBy"
                        },
                        "label": "Total Time Spent (Hrs)",
                        "metric": "total_content_plays_on_app"
                    }
                ],
                "output": [
                    {
                        "dims": [
                            "date",
                            "state"
                        ],
                        "fileParameters": [
                            "id",
                            "dims"
                        ],
                        "metrics": [
                            "total_content_plays_on_portal",
                            "total_content_plays_on_app"
                        ],
                        "type": "csv"
                    }
                ],
                "queryType": "groupBy"
            },
            "store": "azure",
            "streamQuery": true
        },
        "createdOn": 1717153376730,
        "reportDescription": "Course Adoption Report",
        "reportId": "course_adoption_report_plays_and_time_spent",
        "reportSchedule": "DAILY",
        "requestedBy": "fca2925f-1eee-4654-9177-fece3fd6afc9",
        "status": "ACTIVE",
        "status_msg": "REPORT SUCCESSFULLY ACTIVATED",
        "submittedOn": 1717153376730,
        "updatedOn": 1717153376730
    },
    "ts": "2024-06-14T10:02:45.092+00:00",
    "ver": "1.0"
}
```

