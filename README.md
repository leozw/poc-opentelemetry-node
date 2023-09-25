# **📊 OpenTelemetry Collector com Docker & Node.js**

Este guia explica como rodar sua aplicação Node.js junto com o OpenTelemetry Collector utilizando Docker.

## **Pré-requisitos**

- Docker e Docker Compose instalados.
- Uma conta no Grafana para obter as credenciais necessárias.

## **Configurando e Executando com Docker 🐳**

### **1. Arquivo de configuração do OpenTelemetry Collector:**

- Abra ou crie o arquivo **`otel-collector-config.yaml`** no seu diretório.
- Substitua o **`endpoint`** e o cabeçalho **`Authorization`** com suas próprias credenciais do Grafana:

```yaml
otlp:
  endpoint: https://YOUR_GRAFANA_TEMPO_ENDPOINT
  headers:
    Authorization: Basic CONVERTED_TO_BASE64 (INSTANCEID:APIKEY) 
prometheusremotewrite:
  endpoint: https://INSTANCEID:APIKEY@YOUR_GRAFANA_PROMETHEUSREMOTEWRITE_ENDPOINT

```

🚀 **Atenção**: Converta suas credenciais do Grafana para Base64 e use no lugar de **`CONVERTED_TO_BASE64`**. Para o **`prometheusremotewrite`**, não precisa da conversão.

### **2. Preparação do Dockerfile:**

Seu Dockerfile está pronto para construir a imagem da sua aplicação em um ambiente Node.js. Lembre-se que ele expõe a porta **`9191`**.

### **3. Construindo e Executando com Docker Compose:**

- Com base no diretório onde o **`docker-compose.yml`** está localizado, construa as imagens Docker:

```bash
docker-compose build

```

- Após a construção, inicie os serviços:

```bash
docker-compose up

```

- Agora, acesse sua aplicação no navegador através da URL: **`http://localhost:9191`**.
- Depois de testar, pare os serviços:

```bash
docker-compose down

```

---

Com isso, sua aplicação Node.js estará rodando junto com o OpenTelemetry Collector no Docker, e estará enviando dados de telemetria para o Grafana. Se encontrar qualquer problema ou tiver alguma sugestão, não hesite em contribuir! 🚀

---

# **📈 Visualizando Métricas no Grafana**

Depois de rodar sua aplicação e o OpenTelemetry Collector, os dados coletados são enviados ao Grafana. Agora, é hora de visualizá-los!

## **Passos para Visualização:**

### **1. Acesse o Grafana:**

- Acesse sua instância Grafana via navegador usando o link fornecido ao registrar-se ou o que você configurou.

### **2. Explore suas métricas e rastreamentos:**

- No menu lateral, clique em **`🔍 Explore`**.
- Selecione a fonte de dados (Prometheus/Tempo) que você deseja consultar.
- Comece a visualizar suas métricas e rastreamentos. Você pode usar as consultas integradas ou escrever suas próprias consultas para visualizar informações específicas.

### **3. Crie Dashboards Personalizados:**

- Grafana oferece a capacidade de criar painéis personalizados para visualizar seus dados de maneira mais estruturada.
- No menu lateral, clique em **`+`** e selecione **`Dashboard`**.
- Comece a adicionar gráficos e outros elementos visuais ao seu painel para ter uma visão clara dos seus dados de telemetria.

---

Espero que isso ajude a tornar seu guia ainda mais completo! Isso dará a quem lê uma boa ideia de todo o fluxo, desde a coleta de dados até a visualização no Grafana. 📊🚀
