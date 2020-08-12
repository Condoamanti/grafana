# TeamCity Dashboard
Grafana dashboard configuration for TeamCity metrics

### ***Requirements:***
1. TeamCity Enterprise 2019.2+
	- Bearer token created for service user.

### ***Metrics Captured:***
- server_uptime_milliseconds
- buildConfigurations_number
- projects_active_number
- vcsRoots_number
- cpu_count_number
- agents_connected_authorized_number
- builds_running_number
- builds_queued_number
- jvm_memory_used_bytes{id='PS Eden Space'}
- jvm_memory_used_bytes{id='PS Old Gen'}
- jvm_memory_used_bytes{id='PS Survivor Space'}
- jvm_memory_used_bytes{id='Code Cache'}
- jvm_memory_used_bytes{id='Compressed Class Space'}
- jvm_memory_used_bytes{id='Metaspace'}
- httpSessions_active_number
- users_active_number
- jvm_threads_number

### ***Collector Configuration:***
- [/opt/prometheus/prometheus.yml](opt/prometheus/prometheus.yml)

```
  - job_name: "teamcity"
    metrics_path: "/app/metrics"
    scheme: https
    static_configs:
    - targets: ['teamcity.domain.local']
    tls_config:
      insecure_skip_verify: true
    bearer_token: "<SCRUBBED>"
```
### ***GitHub Repository:***
- [https://github.com/Condoamanti/grafana/tree/master/dashboard/teamcity](https://github.com/Condoamanti/grafana/tree/master/dashboard/teamcity)
