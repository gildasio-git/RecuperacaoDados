# 🛠️ Recuperação de Dados com Linux (Fluxo Profissional com ddrescue)

## 📌 Objetivo

Realizar a recuperação de dados de uma mídia com falhas utilizando Linux, preservando integridade e minimizando riscos.

---

# 🔍 1. Diagnóstico inicial

## Identificar o dispositivo

```bash
lsblk
```

ou

```bash
fdisk -l
```

📌 Objetivo:

* Identificar o disco (ex: `/dev/sdX`)
* Verificar partições e estado geral

---

# 📂 2. Montagem inicial (se possível)

```bash
mount /dev/sdX1 /mnt/teste
```

📌 Caso funcione:

* listar arquivos
* avaliar integridade

---

# ⚠️ 3. Problemas de leitura detectados

Sintomas:

* travamentos
* arquivos não copiam
* erros de I/O

👉 **NÃO continuar cópia direta**

---

# 🔥 4. Clonagem com ddrescue (ETAPA CRÍTICA)

## Comando utilizado:

```bash
ddrescue -f -n /dev/sdX imagem.img mapa.log
```

---

## 🧠 Explicação dos parâmetros

| Parâmetro    | Função                                                      |
| ------------ | ----------------------------------------------------------- |
| `-f`         | força escrita no arquivo de saída                           |
| `-n`         | primeira passada rápida (não tenta recuperar setores ruins) |
| `/dev/sdX`   | disco de origem com problema                                |
| `imagem.img` | arquivo de destino (imagem do disco)                        |
| `mapa.log`   | log de progresso e setores                                  |

---

📌 Resultado:

* imagem do disco criada com máxima leitura possível
* setores ruins registrados no log

---

# 💽 5. Mapear imagem como disco (loop device)

```bash
losetup -Pf imagem.img
```

---

## 🧠 Parâmetros

| Parâmetro | Função                             |
| --------- | ---------------------------------- |
| `-f`      | usa loop livre automaticamente     |
| `-P`      | detecta partições dentro da imagem |

---

## Verificar dispositivos criados

```bash
lsblk
```

Exemplo:

```plaintext
/dev/loop0
/dev/loop0p1
```

---

# 📂 6. Montar a partição correta

```bash
mount -o ro /dev/loop0p1 /mnt/recuperacao
```

---

## 🧠 Parâmetros

| Parâmetro      | Função                        |
| -------------- | ----------------------------- |
| `-o ro`        | monta em modo somente leitura |
| `/dev/loop0p1` | partição correta da imagem    |

---

📌 Observação:

* evita corrupção adicional
* mantém integridade dos dados

---

# 🔤 7. Problemas com acentuação

Sintoma:

* nomes de arquivos com caracteres estranhos

👉 Causa:

* encoding incorreto na montagem

---

# 📦 8. Cópia dos dados com rsync

## Comando utilizado:

```bash
rsync -avh --progress --ignore-errors --partial --inplace --no-whole-file /mnt/recuperacao/ /mnt/hd_interno/backup/
```

---

## 🧠 Explicação dos parâmetros

| Parâmetro         | Função                            |
| ----------------- | --------------------------------- |
| `-a`              | modo arquivo (preserva estrutura) |
| `-v`              | modo verbose                      |
| `-h`              | formato legível                   |
| `--progress`      | mostra progresso                  |
| `--ignore-errors` | continua mesmo com erro           |
| `--partial`       | mantém arquivos incompletos       |
| `--inplace`       | escreve direto no destino         |
| `--no-whole-file` | otimiza cópia em discos locais    |

---

📌 Resultado:

* dados copiados mesmo com falhas
* máxima recuperação possível

---

# ⚠️ Observação importante

Durante a cópia:

* pastas podem aparecer vazias inicialmente
* arquivos são preenchidos progressivamente

👉 comportamento normal

---

# 🔍 9. Validação dos arquivos

## Teste de leitura completa

```bash
find /mnt/hd_interno/backup -type f -exec cat {} > /dev/null \;
```

---

📌 Objetivo:

* identificar arquivos corrompidos
* garantir integridade

---

# 📊 10. Análise final

* total de dados: ~200GB
* taxa de sucesso: 100%
* arquivos íntegros

---

# 📄 11. Geração de relatório

Inclui:

* total de arquivos
* tamanho total
* estrutura de diretórios
* status da recuperação

---

# 📦 12. Entrega final

Estrutura recomendada:

```plaintext
backup_final/
 ├── dados recuperados
 ├── relatorio_recuperacao.html
 └── estrutura.txt
```

---

# 🔐 Boas práticas aplicadas

✔️ Nunca trabalhar direto no disco original
✔️ Usar ddrescue para clonagem segura
✔️ Trabalhar sempre em cópia (imagem)
✔️ Montar em modo somente leitura
✔️ Validar dados antes da entrega

---

# 🏁 Conclusão

O processo realizado seguiu padrão profissional de recuperação:

* clonagem segura
* análise via imagem
* recuperação com tolerância a falhas
* validação completa
* documentação final

---

# 🚀 Nível técnico

👉 Esse procedimento é equivalente ao utilizado por empresas especializadas em recuperação de dados.

---
