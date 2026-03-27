# 🛠️ Tutorial de Recuperação Lógica de Dados (Nível Laboratório)

## Objetivo
Recuperar dados de mídia com falhas de leitura utilizando ddrescue e rsync em múltiplas fases.

---

## FASE 1 — Setores Saudáveis

### Comando
ddrescue -f -n -c 64 /dev/sdX imagem.img mapa.log

### Parâmetros
- -f: força sobrescrita
- -n: ignora setores ruins (rápido)
- -c 64: lê blocos maiores (performance)

---

## FASE 2 — Setores Danificados

### Comando
ddrescue -d -r1 -c 1 /dev/sdX imagem.img mapa.log

### Parâmetros
- -d: acesso direto ao disco
- -r1: tenta 1 vez setores ruins
- -c 1: leitura setor a setor

---

## FASE 3 — Leitura Reversa

### Comando
ddrescue -R -d -r1 /dev/sdX imagem.img mapa.log

### Parâmetros
- -R: leitura reversa
- -d: acesso direto
- -r1: tentativa adicional

---

## FASE 4 — Montagem

mkdir /mnt/recuperado
mount -o loop,ro imagem.img /mnt/recuperado

---

## FASE 5 — Cópia com rsync

rsync -rltv --ignore-errors --no-perms --no-owner --no-group --timeout=120 --partial --inplace /mnt/recuperado/ /destino/

---

## Logs

- erros: 2>>erros.log
- sucesso: >>copiados.log

---

## Conclusão
1. Recuperar setores bons
2. Tentar setores ruins
3. Leitura reversa
4. Copiar arquivos
