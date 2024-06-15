# Enterprise IT Architecture
adapting 'Manajemen Infrastruktur' Final Project, this is the architecture I plan to implement. Containerized microservices.
![IT architecture](./images/enterprise-infra.jpg)

- [Architecture](#architecture)
    - [Database Server](#database-server)
    - [E-commerce Server 1 & 2](#e-commerce-server-1--2)
    - [Load Balancer E-commerce Server](#load-balancer-e-commerce-server)
    - [Internal ERP Server 1 & 2](#internal-erp-server-1--2)
    - [Load Balancer Internal ERP Server](#load-balancer-internal-erp-server)
    - [File Server](#file-server)
    - [LDAP Server](#ldap-server)
    - [Monitoring Server](#monitoring-server)

## Architecture
### Database Server
Host dari sistem database terintegrasi PostgreSQL. Sistem database ini terintegrasi untuk semua aplikasi perusahaan yang memiliki dependensi kepada suatu database, seperti Odoo dan NextCloud.

### E-commerce Server 1 & 2
Host dari aplikasi *e-commerce* milik perusahaan. *E-commerce* dibangun menggunakan Odoo 16 di dalam sebuah kontainer Docker dan bisa diakses oleh publik.

### Load Balancer E-commerce Server
Host dari *load balancer* kedua server *e-commerce*. Aplikasi *load balancer* memanfaatkan Nginx yang di-*deploy* di dalam kontainer Docker.

### Internal ERP Server 1 & 2
Host dari aplikasi *internal ERP* milik perusahaan. ERP juga menggunakan Odoo 16 dan terhubung ke sistem database yang sama dengan Odoo untuk *e-commerce*. Aplikasi ERP di-deploy di dalam kontainer Docker dan hanya bisa diakses oleh device yang berada di jaringan perusahaan.

### Load Balancer Internal ERP Server
Host dari *load balancer* kedua server ERP. *Load balancer* ini juga memanfaatkan Nginx yang di deploy di dalam kontainer Docker.

### File Server
Host dari aplikasi NextCloud sebagai *file sharing system* perusahaan. Aplikasi di-*deploy* di dalam kontainer Docker dan bisa diakses oleh publik. Autentikasi menggunakan sistem LDAP.

### LDAP Server
Host dari sistem autentikasi LDAP untuk NextCloud dan Odoo 16 untuk internal ERP.

### Monitoring Server
Host dari sistem monitoring infrastruktur yang akan dibangun. Digunakan Promotheus-Grafana yang di deploy di kontainer Docker masing-masing. Data monitoring di-*scrapping* oleh Promotheus dari Node Exporter dan cAdvisor yang di-*deploy* di dalam kontainer Docker server-server lainnya dan divisualisasikan oleh Grafana.