# **Введение**

В данном домашнем задании нам необходимо получить практический начальный опыт работы с Prometheus .

---

# **Создание собстенного Dashboard **

1. Для выполнения этого задания были разыёрнуты (а точнее использованы ранее настроенные с курса basic) виртуальные машины, на которых были установлены и настроены Prometheus и Grafana, с установкой node_exporter. Так выглядит файл настройки prometheus.yml.
```
[dima@Test-Centos7-1 ~]$ cat /etc/prometheus/prometheus.yml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'mysql_exporter_fosslinux'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9104']

  - job_name: 'node_exporter_Test_Centos7_2'
    scrape_interval: 5s
    static_configs:
      - targets: ['10.10.62.5:9100']

  - job_name: 'mysql_exporter_fosslinux_Test_Centos7_2'
    scrape_interval: 5s
    static_configs:
      - targets: ['10.10.62.5:9104']
```
2. На курсе Basic - сами Dashboard были взяты с сайта Grafana - `https://grafana.com/grafana/dashboards/`.
В этот раз, я воспользовался данным кратким видео - `https://www.youtube.com/watch?v=YUabB_7H710`, по настройки как раз нужных нам 4-ёх графикоф на своём Dashboard.
Также подсмотрел в `Query` графиков с готовых шаблонов, скачанных под node-exporter. В итоге получился такой Dashboard (чтобы графики не выглядели статично, так как машины работают без нагрузки - пришлось погонять утилиту streess и сделать несколько закачек фоайлов).
![alt text](/screenshots/hw14-1.PNG?raw=true "Screenshot1")