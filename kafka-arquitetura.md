# Arquitetura do Kafka com Tópicos LOCATIONS e EQUIPMENTS

Este documento descreve a arquitetura de um sistema baseado no Kafka, com foco nos tópicos **LOCATIONS** e **EQUIPMENTS**, responsáveis por armazenar dados de diferentes módulos e eventos relacionados.

## Estrutura Geral

O Kafka é utilizado como a principal plataforma de mensageria e streaming de dados entre os diferentes módulos do sistema. Cada tópico é configurado para receber, armazenar e distribuir mensagens estruturadas no formato JSON, facilitando a integração entre sistemas.

---

## Tópico: LOCATIONS

### Descrição

Responsável por armazenar os dados relacionados à organização espacial e hierárquica das plantas, fábricas, departamentos, centros de custo, locais e tags.

### Exemplos de Dados Armazenados

- Plantas
- Fábricas
- Departamentos
- Centros de custo
- Locais
- Tags

### Formato da Mensagem

```json
{
  "message_id": "1733447603805-equipment_service-a19a3f",
  "timestamp": "2024-12-06T01:13:23.805Z",
  "source_system": "equipment_service",
  "destination_system": "voyager-2",
  "event_type": "plant_registration",
  "user": "admin",
  "payload": {
    "name": "THOR",
    "status": true
  }
}
```

## Tópico: EQUIPMENTS

### Descrição

Responsável por armazenar os dados relacionados aos equipamentos, incluindo suas movimentações, modelos e associações.

### Exemplos de Dados Armazenados

- Siglas
- Fabricante
- Modelos
- Equipamentos
- Movimentações

### Formato da Mensagem

```json
{
  "message_id": "1733448275747-equipment_service-94a59a",
  "timestamp": "2024-12-06T01:24:35.747Z",
  "source_system": "equipment_service",
  "destination_system": "voyager-2",
  "event_type": "types_registration",
  "user": "admin",
  "payload": {
    "name": "THOR",
    "initials": "THO",
    "status": true
  }
}
```

## Estrutura do Payload

Ambos os tópicos compartilham um padrão de mensagem que facilita a integração e rastreabilidade.

### Campos Gerais

- **message_id**: Identificador único da mensagem, combinando timestamp, sistema de origem e ID único.
- **timestamp**: Data e hora do evento no formato ISO 8601.
- **source_system**: Nome do sistema que originou o evento.
- **destination_system**: Nome do sistema de destino.
- **event_type**: Tipo do evento ocorrido (e.g., `plant_registration`, `plant_modification` e `plant_removal`).
- **user**: Usuário responsável pela alteração.

### Payload Específico

- **LOCATIONS**: Contém informações sobre locais e suas associações.
- **EQUIPMENTS**: Inclui dados sobre equipamentos e movimentações.

![alt text](imagem-arquitetura-1.png)

![alt text](kafka-topics-1.png)
