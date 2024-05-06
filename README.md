# training-es

Dockerized two-nodes Elasticsearch cluster with Kibana and the following plugins installed:
- analysis-icu
- analysis-stempel
- pl.allegro.tech.elasticsearch.plugin:elasticsearch-analysis-morfologik
- ingest-attachment

## Usage
1. Build custom Elasticsearch image (with listed plugins installed):
   ```
   docker build -f elasticsearch-with-plugins -t training-es:8.13.3 .
   ```

2. Setup docker-machine by increasing limits on mmap counts corresponding to https://elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html
\
   1. For **Windows** users running Docker on WSL2 requires increasing mmap counts (after every Docker/WSL2 reboot)
      ```
      wsl -d docker-desktop
      sysctl -w vm.max_map_count=262144
      ```
   
   2. For **MacOS with Colima** it can be done permanently:
      ```
      colima start --edit
      ```
      Replace default configuration for `provision` element with
      ```
      provision:
          - mode: system
            script: sysctl -w vm.max_map_count=262144
      ```

3. Start cluster using this command:
   ```
   docker-compose up
   ```

4. Open http://localhost:5601 in your favourite browser and start using Kibana ;-)
