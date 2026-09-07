# Data Quality Audit and Analysis of a Long-Term LoRaWAN Network: Anomaly Detection, PCA, Clustering and Machine Learning

## Context and Operational Challenges in Long-Term IoT Monitoring

Long-term environmental monitoring via Low-Power Wide-Area Networks
(LPWAN)---specifically using the LoRaWAN protocol---presents unique data
engineering and data quality challenges. In real-world deployments such
as the Perret Tower (*Tour Perret*) dataset [Donsez et al., raw
telemetry streams suffer from network packet loss, heterogeneous payload
formats, multi-gateway frame duplication, and hardware configuration
shifts over time.

A common pitfall in multivariate anomaly detection and predictive
modeling is the *a priori* assumption of variable co-occurrence.
Researchers and practitioners often design processing pipelines
expecting all target variables---such as Temperature ($T$), Relative
Humidity ($H$), Atmospheric Pressure ($P$), and Carbon Dioxide
concentration ($\mathrm{CO_2}$)---to be present synchronously in every
transmitted frame. However, in multi-sensor LPWAN deployments, distinct
physical sensors often operate on different transmission schedules,
report varying payload schemas across firmware revisions, or belong to
completely separate device applications aggregated under a single
network server instance.

<div>
 <img src="figures/lorawan_pipeline_audit-wt.png" width="800"  style="display:block; margin-botom:10px;">
</div>
