---
layout: center
align: center
transition: fade
--- 

# Timeskip pra 2024

Como vai a vida? Cadê os projetos? Já publicou algo? Tá rico?

> Muita variavel pra pouca constante - Reis, Daniel


---
transition: fade-out
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "ScyllaDB"
full_name: "Developer Advocate"
---


# Developer Relations 101


Developer Relations é a área que faz o desenvolvedor que gosta de participar de comunidades de tecnologia, se sentir acolhido pela marca que ele decidiu apoiar.

<v-click>

Com **"marca"**, eu me refiro à empresas que vendem produto para desenvolvedores e você pode pensar em:

- Clouds (AWS, GCP, MagaluCloud, Azure etc)
- Frameworks (React, Laravel, Spring, Rails etc)
- Banco de Dados (ScyllaDB, MySQL, Redis etc)
- Comunidades (Forum, Discord, Redes Sociais)
- Eventos (RogaDX, Front-in Sampa, CityJS, Laracon)
</v-click>


<v-click>

Então no geral, podemos entender que:

</v-click>

<div class="mt-5" v-click>

> DevRel: Pessoa desenvolvedora que faz marketing de um produto para desenvolvedores que querem aprender sobre por motivos.

</div>



---
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "ScyllaDB"
full_name: "Developer Advocate"
---


# Developer Advocate

Meu trabalho então é engajar comunidades e fazer eles conhecerem isso aqui ó:


<v-clicks>

* ScyllaDB: 
  * Banco de Dados Distribuido NoSQL de Alta Performance
  * Feito em C++ (Gerenciamento de Memória Custom)
  * Shard-aware > Threads
  * Arquitetado baseado nas boas partes do CassandraDB (CQL) e do DynamoDB.
* Para leigos:
  * CQL = SQL só que você só consulta baseado em indexes;
  * ScyllaDB faz "substituição imediata" com bancos como CassandraDB e DynamoDB por ter implementado os protocolos deles tendo performance superior. 


</v-clicks>

---
layout: image
image: https://i.imgur.com/8hvT8ze.png
---

---
layout: image
image: https://i.imgur.com/QHa3L3S.png
---
---
transition: none
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "ScyllaDB"
full_name: "Developer Advocate"
---


# Developer Advocate

Mas também meu trabalho é engajar comunidades na ideia de:

- Promover código aberto pra comunidade local
- Criar e Contribuir em amostras/projetos usando ScyllaDB
- Participar de eventos ao redor do mundo
- Fazer Lives aprendendo e ensinando tecnologias como:

<v-click>
```rust
// Rust
#[charybdis_model(
    table_name = user_metrics_v1,
    partition_keys = [user_id],
    clustering_keys = [],
    global_secondary_indexes = [],
)]
#[derive(Debug, Serialize, Deserialize, Default, Clone)]
pub struct UserMetrics {
  pub user_id: Int,
  pub minutes_watched: Option<Counter>,
  pub messages_count: Option<Counter>,
}
```
</v-click>

---
transition: none
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "ScyllaDB"
full_name: "Developer Advocate"
---


# Developer Advocate

Mas também meu trabalho é engajar comunidades na ideia de:

- Promover código aberto pra comunidade local
- Criar e Contribuir em amostras/projetos usando ScyllaDB
- Participar de eventos ao redor do mundo
- Fazer Lives aprendendo e ensinando tecnologias como:


```cql
// ScyllaDB CQL
CREATE TABLE twitch.user_metrics_v1 (
    user_id int,
    messages_count counter,
    minutes_watched counter,
    PRIMARY KEY (user_id)
) WITH bloom_filter_fp_chance = 0.01
    AND caching = {'keys': 'ALL','rows_per_partition': 'ALL'}
    AND comment = ''
    AND compaction = {'class': 'IncrementalCompactionStrategy'}
    AND compression = {'sstable_compression': 'org.apache.LZ4Compressor'}
    AND dclocal_read_repair_chance = 0
    AND default_time_to_live = 0;
```

---
transition: fade
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "ScyllaDB"
full_name: "Developer Advocate"
---

# Developer Advocate

Mas também meu trabalho é engajar comunidades na ideia de:

- Promover código aberto pra comunidade local
- Criar e Contribuir em amostras/projetos usando ScyllaDB
- Participar de eventos ao redor do mundo
- Fazer Lives aprendendo e ensinando tecnologias como:


```yml
# Docker - thx @gvieira18
services:
  scylla-1: &scylla-main
    image: scylladb/scylla:6.1
    container_name: scylla-1
    command:
      - --smp=2
      - --memory=2GB
      - --overprovisioned=1
      - --developer-mode=1
      - --seeds=scylla-1
    ports:
      - "9042:9042"
```


---
transition: zoom
layout: whoami
image: "https://i.imgur.com/f67pUvn.png"
handle: "Criando algo pra escalar em 1M/IOPS"
full_name: "Task foda"
---

# Nova Tarefa: Criar uma amostra KV pra 1M req/s

Bom, eu trabalho num banco de dados de alta performance, então tudo que eu desenvolvo é planejando escalar baseado na necessidade do usuário!

Porém, sua cabeça, o que seria prioridade nessas aplicações de alta demanda? 

<v-click>

> Resposta curta: paginas que são acessadas com recorrencia!

Deixa eu te dar alguns exemplos de empresas que usam pra tu ter uma noção:

</v-click>


---
transition: zoom
layout: whoami
image: "https://i.imgur.com/f67pUvn.png"

---

# Casos de Uso

Empresa: Discord


![discord](https://cdn.prod.website-files.com/5f9072399b2640f14d6a2bf4/640658a746a8ce16d18f27ac_027_Header.png)


[Como o Discord armazena trilhões de mensagens?](https://discord.com/blog/how-discord-stores-trillions-of-messages)

<div class="mt-4 mb-4">
Artigo por: Bo Ingram - 6 de março de 2023
</div>


> TLDR: usando ScyllaDB =D

---
transition: zoom
layout: whoami
image: "https://i.imgur.com/f67pUvn.png"
---

# Casos de Uso

Empresa: iFood


![ifood](https://i.imgur.com/4wqCYEZ.png)


[iFood conta com ScyllaDB para entregar mais de 100 milhões de eventos por mês para restaurantes](https://www.scylladb.com/2020/04/16/ifood-relies-on-scylla-to-deliver-over-100-million-events-a-month-to-restaurants/)

<div class="mt-4 mb-4">
Artigo por: Peter Corless - 16 de Abril de 2020
</div>


> TLDR: usando ScyllaDB =D



---
transition: zoom
layout: whoami
image: "https://i.imgur.com/f67pUvn.png"

---

# Casos de Uso

Entre alguns outros: [scylladb.com/users](https://scylladb.com/users)

<div class="">

![casos](https://i.imgur.com/ojmeyeZ.png)

</div>