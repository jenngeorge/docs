## Statements table

Click **Columns** to select the columns to display in the table.

The Statements table gives details for each SQL statement fingerprint:

Column | Description
-----|------------
Statements | SQL statement [fingerprint](#sql-statement-fingerprints). To view additional details, click the SQL statement fingerprint to open its [Statement Fingerprint page]({{ page_prefix }}statements-page.html#statement-fingerprint-page).
Execution Count | Cumulative number of executions of statements with this fingerprint within the [time interval](#time-interval). <br><br>The bar indicates the ratio of runtime success (gray) to [retries]({{ link_prefix }}transactions.html#transaction-retries) (red) for the SQL statement fingerprint.
Database | The database in which the statement was executed.
Application Name | The name specified by the [`application_name`]({{ link_prefix }}show-vars.html#supported-variables) session setting.
Statement Time | Average [planning and execution time]({{ link_prefix }}architecture/sql-layer.html#sql-parser-planner-executor) of statements with this statement fingerprint within the time interval. <br><br>The gray bar indicates the mean latency. The blue bar indicates one standard deviation from the mean. Hover over the bar to display exact values.
% of All Runtime | How much time this statement fingerprint took to execute compared to all other statements that were executed within the time period. It is expressed as a percentage. The runtime is the mean execution latency multiplied by the execution count.
Contention Time | Average time statements with this fingerprint were [in contention]({{ link_prefix }}performance-best-practices-overview.html#understanding-and-avoiding-transaction-contention) with other transactions within the time interval.<br><br>The gray bar indicates mean contention time. The blue bar indicates one standard deviation from the mean. Hover over the bar to display exact values.
CPU Time | Average CPU time spent executing within the specified time interval. The gray bar indicates mean CPU time. The blue bar indicates one standard deviation from the mean. <br><br>The CPU time includes time spent in the [SQL layer](architecture/sql-layer.html). It does not include time spent in the [storage layer](architecture/storage-layer.html).
P50 Latency | The 50th latency percentile for sampled statement executions with this fingerprint.
P90 Latency | The 90th latency percentile for sampled statement executions with this fingerprint.
P99 Latency | The 99th latency percentile for sampled statement executions with this fingerprint.
Min Latency | The lowest latency value for all statement executions with this fingerprint.
Max Latency | The highest latency value for all statement executions with this fingerprint.
Rows Processed | Average number of rows read and written while executing statements with this fingerprint within the time interval.
Bytes Read | Aggregation of all bytes [read from disk]({{ link_prefix }}architecture/life-of-a-distributed-transaction.html#reads-from-the-storage-layer) across all operators for statements with this fingerprint within the time interval. <br><br>The gray bar indicates the mean number of bytes read from disk. The blue bar indicates one standard deviation from the mean. Hover over the bar to display exact values.
Max Memory | Maximum memory used by a statement with this fingerprint at any time during its execution within the time interval. <br><br>The gray bar indicates the average max memory usage. The blue bar indicates one standard deviation from the mean. Hover over the bar to display exact values.
Network | Amount of [data transferred over the network]({{ link_prefix }}architecture/reads-and-writes-overview.html) for statements with this fingerprint within the time interval. If this value is 0, the statement was executed on a single node. <br><br>The gray bar indicates the mean number of bytes sent over the network. The blue bar indicates one standard deviation from the mean. Hover over the bar to display exact values.
Retries | Cumulative number of automatic (internal) [retries]({{ link_prefix }}transactions.html#transaction-retries) by CockroachDB of statements with this fingerprint within the time interval.
Regions/Nodes | The regions and nodes on which statements with this fingerprint executed. <br><br>Nodes are not visible for {{ site.data.products.serverless }} clusters or for clusters that are not multi-region.
Last Execution Time (UTC)| The timestamp when the statement was last executed.
Statement Fingerprint ID | The ID of the statement fingerprint.
Diagnostics | Activate and download [diagnostics](#diagnostics) for this fingerprint. To activate, click the **Activate** button. The [Activate statement diagnostics](#activate-diagnostics-collection-and-download-bundles) dialog displays. After you complete the dialog, the column displays the status of diagnostics collection (**WAITING**, **READY**, or **ERROR**). Click <img src="{{ 'images/common/ui-ellipsis-button.png' | relative_url }}" alt="Vertical ellipsis" /> and select a bundle to download or select **Cancel request** to cancel diagnostics bundle collection. <br><br>Statements are periodically cleared from the Statements page based on the start time. To access the full history of diagnostics for the fingerprint, see the [Diagnostics](#diagnostics) tab of the Statement Details page. <br><br>Diagnostics is not visible for {{ site.data.products.serverless }} clusters.

{{site.data.alerts.callout_info}}
To obtain the execution statistics, CockroachDB samples a percentage of the executions. If you see `no samples` displayed in the **Contention**, **Max Memory**, or **Network** columns, there are two possibilities:
- Your statement executed successfully but wasn't sampled because there were too few executions of the statement.
- Your statement has failed (the most likely case). You can confirm by clicking the statement and viewing the value for **Failed?**.
{{site.data.alerts.end}}

To view statement details, click a SQL statement fingerprint in the **Statements** column to open the **Statement Fingerprint** page.
