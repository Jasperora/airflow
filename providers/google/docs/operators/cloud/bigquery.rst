 .. Licensed to the Apache Software Foundation (ASF) under one
 .. Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

 ..   http://www.apache.org/licenses/LICENSE-2.0

 .. Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

Google Cloud BigQuery Operators
===============================

`BigQuery <https://cloud.google.com/bigquery/>`__ is Google's fully managed, petabyte
scale, low cost analytics data warehouse. It is a serverless Software as a Service
(SaaS) that doesn't need a database administrator. It allows users to focus on
analyzing data to find meaningful insights using familiar SQL.

Airflow provides operators to manage datasets and tables, run queries and validate
data.

Prerequisite Tasks
^^^^^^^^^^^^^^^^^^

.. include:: /operators/_partials/prerequisite_tasks.rst

Manage datasets
^^^^^^^^^^^^^^^

.. _howto/operator:BigQueryCreateEmptyDatasetOperator:

Create dataset
""""""""""""""

To create an empty dataset in a BigQuery database you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryCreateEmptyDatasetOperator`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_create_dataset]
    :end-before: [END howto_operator_bigquery_create_dataset]

.. _howto/operator:BigQueryGetDatasetOperator:

Get dataset details
"""""""""""""""""""

To get the details of an existing dataset you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryGetDatasetOperator`.

This operator returns a `Dataset Resource <https://cloud.google.com/bigquery/docs/reference/rest/v2/datasets#resource>`__.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_get_dataset]
    :end-before: [END howto_operator_bigquery_get_dataset]

.. _howto/operator:BigQueryGetDatasetTablesOperator:

List tables in dataset
""""""""""""""""""""""

To retrieve the list of tables in a given dataset use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryGetDatasetTablesOperator`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_get_dataset_tables]
    :end-before: [END howto_operator_bigquery_get_dataset_tables]

.. _howto/operator:BigQueryUpdateTableOperator:

Update table
""""""""""""""

To update a table in BigQuery you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryUpdateTableOperator`.

The update method replaces the entire Table resource, whereas the patch
method only replaces fields that are provided in the submitted Table resource.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_update_table]
    :end-before: [END howto_operator_bigquery_update_table]

You can use this operator to update a view.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_update_view]
    :end-before: [END howto_operator_bigquery_update_view]

And use the same operator to update a materialized view.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_update_materialized_view]
    :end-before: [END howto_operator_bigquery_update_materialized_view]

.. _howto/operator:BigQueryUpdateDatasetOperator:

Update dataset
""""""""""""""

To update a dataset in BigQuery you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryUpdateDatasetOperator`.

The update method replaces the entire dataset resource, whereas the patch
method only replaces fields that are provided in the submitted dataset resource.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_update_dataset]
    :end-before: [END howto_operator_bigquery_update_dataset]

.. _howto/operator:BigQueryDeleteDatasetOperator:

Delete dataset
""""""""""""""

To delete an existing dataset from a BigQuery database you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryDeleteDatasetOperator`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_dataset.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_delete_dataset]
    :end-before: [END howto_operator_bigquery_delete_dataset]

Manage tables
^^^^^^^^^^^^^

.. _howto/operator:BigQueryCreateTableOperator:

Create table
""""""""""""

To create a new table in a dataset with the data in Google Cloud Storage
you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryCreateTableOperator` by providing `table structure <https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#resource:-table>`__
in ``table_resource`` field.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_create_table]
    :end-before: [END howto_operator_bigquery_create_table]

You can also specify Google Cloud Storage object name as a way to specify schema. The object in Google Cloud
Storage must be a JSON file with the schema fields in it.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_create_table_schema_json]
    :end-before: [END howto_operator_bigquery_create_table_schema_json]

You can use this operator to create a view on top of an existing table.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_create_view]
    :end-before: [END howto_operator_bigquery_create_view]

You can also use this operator to create a materialized view that periodically
caches results of a query for increased performance and efficiency.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_create_materialized_view]
    :end-before: [END howto_operator_bigquery_create_materialized_view]

.. _howto/operator:BigQueryGetDataOperator:

Fetch data from table
"""""""""""""""""""""

To fetch data from a BigQuery table you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryGetDataOperator` .
Alternatively you can fetch data for selected columns if you pass fields to
``selected_fields``.

The result of this operator can be retrieved in two different formats based on the value of the ``as_dict`` parameter:
``False`` (default) - A Python list of lists, where the number of elements in the nesting list will be equal to the number of rows fetched. Each element in the
nesting will a nested list where elements would represent the column values for
that row.
``True`` - A Python list of dictionaries, where each dictionary represents a row. In each dictionary, the keys are the column names and the values are the corresponding values for those columns.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_get_data]
    :end-before: [END howto_operator_bigquery_get_data]

The below example shows how to use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryGetDataOperator`
in async (deferrable) mode. Note that a deferrable task requires the Triggerer to be
running on your Airflow deployment.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_get_data_async]
    :end-before: [END howto_operator_bigquery_get_data_async]

.. _howto/operator:BigQueryUpsertTableOperator:

Upsert table
""""""""""""

To upsert a table you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryUpsertTableOperator`.

This operator either updates the existing table or creates a new, empty table
in the given dataset.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_upsert_table]
    :end-before: [END howto_operator_bigquery_upsert_table]

.. _howto/operator:BigQueryUpdateTableSchemaOperator:

Update table schema
"""""""""""""""""""

To update the schema of a table you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryUpdateTableSchemaOperator`.

This operator updates the schema field values supplied, while leaving the rest unchanged. This is useful
for instance to set new field descriptions on an existing table schema.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_update_table_schema]
    :end-before: [END howto_operator_bigquery_update_table_schema]

.. _howto/operator:BigQueryDeleteTableOperator:

Delete table
""""""""""""

To delete an existing table you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryDeleteTableOperator`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_delete_table]
    :end-before: [END howto_operator_bigquery_delete_table]

You can also use this operator to delete a view.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_delete_view]
    :end-before: [END howto_operator_bigquery_delete_view]

You can also use this operator to delete a materialized view.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_tables.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_delete_materialized_view]
    :end-before: [END howto_operator_bigquery_delete_materialized_view]

.. _howto/operator:BigQueryInsertJobOperator:

Execute BigQuery jobs
^^^^^^^^^^^^^^^^^^^^^

Let's say you would like to execute the following query.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 0
    :start-after: [START howto_operator_bigquery_query]
    :end-before: [END howto_operator_bigquery_query]

To execute the SQL query in a specific BigQuery database you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryInsertJobOperator`
with proper query job configuration that can be Jinja templated.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_insert_job]
    :end-before: [END howto_operator_bigquery_insert_job]

The below example shows how to use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryInsertJobOperator`
in async (deferrable) mode. Note that a deferrable task requires the Triggerer to be
running on your Airflow deployment.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_insert_job_async]
    :end-before: [END howto_operator_bigquery_insert_job_async]

For more information on types of BigQuery job please check
`documentation <https://cloud.google.com/bigquery/docs/reference/v2/jobs>`__.

If you want to include some files in your configuration you can use ``include`` clause of Jinja template
language as follow:

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_select_job]
    :end-before: [END howto_operator_bigquery_select_job]

The included file can also use Jinja templates which can be useful in case of ``.sql`` files.

Additionally you can use ``job_id`` parameter of
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryInsertJobOperator` to improve
idempotency. If this parameter is not passed then uuid will be used as ``job_id``. If provided then
operator will try to submit a new job with this ``job_id```. If there's already a job with such ``job_id``
then it will reattach to the existing job.

Also for all this action you can use operator in the deferrable mode:

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_insert_job_async]
    :end-before: [END howto_operator_bigquery_insert_job_async]

Validate data
^^^^^^^^^^^^^

.. _howto/operator:BigQueryCheckOperator:

Check if query result has data
""""""""""""""""""""""""""""""

To perform checks against BigQuery you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryCheckOperator`

This operator expects a sql query that will return a single row. Each value on
that first row is evaluated using python ``bool`` casting. If any of the values
return ``False`` the check is failed and errors out.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_check]
    :end-before: [END howto_operator_bigquery_check]

Also you can use deferrable mode in this operator

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_check_async]
    :end-before: [END howto_operator_bigquery_check_async]

.. _howto/operator:BigQueryValueCheckOperator:

Compare query result to pass value
""""""""""""""""""""""""""""""""""

To perform a simple value check using sql code you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryValueCheckOperator`

These operators expects a sql query that will return a single row. Each value on
that first row is evaluated against ``pass_value`` which can be either a string
or numeric value. If numeric, you can also specify ``tolerance``.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_value_check]
    :end-before: [END howto_operator_bigquery_value_check]

Also you can use deferrable mode in this operator

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_value_check_async]
    :end-before: [END howto_operator_bigquery_value_check_async]

.. _howto/operator:BigQueryIntervalCheckOperator:

Compare metrics over time
"""""""""""""""""""""""""

To check that the values of metrics given as SQL expressions are within a certain
tolerance of the ones from ``days_back`` before you can either use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryIntervalCheckOperator` or
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryIntervalCheckAsyncOperator`

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_interval_check]
    :end-before: [END howto_operator_bigquery_interval_check]

Also you can use deferrable mode in this operator

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries_async.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_interval_check_async]
    :end-before: [END howto_operator_bigquery_interval_check_async]

.. _howto/operator:BigQueryColumnCheckOperator:

Check columns with predefined tests
"""""""""""""""""""""""""""""""""""

To check that columns pass user-configurable tests you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryColumnCheckOperator`

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_column_check]
    :end-before: [END howto_operator_bigquery_column_check]

.. _howto/operator:BigQueryTableCheckOperator:

Check table level data quality
""""""""""""""""""""""""""""""

To check that tables pass user-defined tests you can use
:class:`~airflow.providers.google.cloud.operators.bigquery.BigQueryTableCheckOperator`

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_queries.py
    :language: python
    :dedent: 4
    :start-after: [START howto_operator_bigquery_table_check]
    :end-before: [END howto_operator_bigquery_table_check]

Sensors
^^^^^^^

Check that a Table exists
"""""""""""""""""""""""""

To check that a table exists you can define a sensor operator. This allows delaying execution
of downstream operators until a table exist. If the table is sharded on dates you can for instance
use the ``{{ ds_nodash }}`` macro as the table name suffix.

:class:`~airflow.providers.google.cloud.sensors.bigquery.BigQueryTableExistenceSensor`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_bigquery_table]
    :end-before: [END howto_sensor_bigquery_table]

Also you can use deferrable mode in this operator if you would like to free up the worker slots while the sensor is running.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_bigquery_table_defered]
    :end-before: [END howto_sensor_bigquery_table_defered]

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_async_bigquery_table]
    :end-before: [END howto_sensor_async_bigquery_table]

Check that a Table Partition exists
"""""""""""""""""""""""""""""""""""

To check that a table exists and has a partition you can use.
:class:`~airflow.providers.google.cloud.sensors.bigquery.BigQueryTablePartitionExistenceSensor`.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_bigquery_table_partition]
    :end-before: [END howto_sensor_bigquery_table_partition]

For DAY partitioned tables, the partition_id parameter is a string on the "%Y%m%d" format

Also you can use deferrable mode in this operator if you would like to free up the worker slots while the sensor is running.

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_bigquery_table_partition_defered]
    :end-before: [END howto_sensor_bigquery_table_partition_defered]

.. exampleinclude:: /../../google/tests/system/google/cloud/bigquery/example_bigquery_sensors.py
    :language: python
    :dedent: 4
    :start-after: [START howto_sensor_bigquery_table_partition_async]
    :end-before: [END howto_sensor_bigquery_table_partition_async]

Reference
^^^^^^^^^

For further information, look at:

* `Client Library Documentation <https://googleapis.dev/python/bigquery/latest/index.html>`__
* `Product Documentation <https://cloud.google.com/bigquery/docs/>`__
