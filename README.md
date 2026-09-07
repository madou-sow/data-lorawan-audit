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

<figcaption>Figure 1: LoRaWAN telemetry ingestion and cleaning pipeline: the
coverage audit (Step 1) is executed before any downstream analysis,
separating structurally unusable variables (CO<span
class="math inline">\(_2\)</span>, pressure) from the retained bivariate
(T,H) core dataset.</figcaption>
</figure>

## Theoretical Framework & Methodology 

### The Need for Multi-Tiered Anomaly Detection in IoT Streams 

Anomalies in environmental time-series data do not manifest as a single
homogeneous class. In edge-computing and IoT sensor contexts, anomalies
span a spectrum of behaviors:

- **Extreme Univariate Outliers:** Sensor spikes, electrical bursts, or
  out-of-spec hardware failures.

- **Multivariate Structural Anomalies:** Observations where each
  individual feature remains within normal seasonal bounds, but their
  *joint combination* violates fundamental physical laws or dominant
  environmental correlations.

- **Density-Based Clustered Anomalies / Noise:** Isolated noise points
  residing in low-density regions of the multivariate feature space.

- **Systemic Temporal Drifts:** Gradual, continuous calibration loss
  (e.g., aging capacitive humidity elements) that evades point-based
  detection because individual readings shift slowly over weeks or
  months.

  <div>
 <img src="figures/cleanBivariate-wt.png" width="800"  style="display:block; margin-botom:10px;">
</div>

<figcaption>Figure 2: Four-tier complementary detection framework: each tier
targets a distinct, orthogonal anomaly signature within the clean
bivariate (T,H) dataset.</figcaption>
</figure>
