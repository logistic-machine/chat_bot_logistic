# # 🤖 Agente de Validação de Notas Fiscais — WMS × SAP

> Agente conversacional em Python que cruza dados de recebimento do WMS e do SAP para responder ao cliente em linguagem natural via API do Claude.

---

## 🧩 O Problema

O processo manual envolvia:
- Exportar reports do WMS e do SAP separadamente
- Cruzar os dados em Excel
- Identificar NFs bloqueadas e o motivo do impedimento
- Montar arquivo de retorno e enviar ao cliente

Resultado: processo lento, manual e sujeito a erro humano.

---

## ✅ A Solução

Um agente inteligente que automatiza o cruzamento e permite ao cliente consultar o status das suas NFs por linguagem natural.

**Exemplos de perguntas que o agente responde:**
- "O pedido de compra 4500123 já foi recebido?"
- "Qual o status da NF do fornecedor X?"
- "Por que o material Y ainda não entrou no estoque?"
- "Quais NFs estão com pendência de validação hoje?"

---

## ⚙️ Como Funciona

```
Report WMS  ──┐
              ├──▶  Script Python  ──▶  SQLite  ──▶  Agente Claude  ──▶  Resposta ao cliente
Report SAP  ──┘
```

1. Os reports do WMS e SAP são carregados e normalizados via **Pandas**
2. Os dados são inseridos num banco **SQLite local** estruturado por NF, pedido de compra, fornecedor e status
3. O agente usa a **API do Claude com tools** para traduzir perguntas em linguagem natural em consultas SQL
4. A resposta é devolvida ao utilizador com o status real da NF — incluindo o motivo do bloqueio, se houver

---

## 🛠️ Stack Técnica

| Tecnologia | Uso |
|---|---|
| Python | Core do projeto |
| Pandas | Leitura e normalização dos reports |
| SQLite | Banco de dados local estruturado |
| API Claude (Anthropic) | Motor do agente conversacional com tools |
| openpyxl / xlwings | Geração do arquivo Excel de retorno |

---

## 🚧 Desafios Encontrados

- **Estrutura do banco:** Definir o schema SQLite ideal para suportar o volume e a variedade de dados de NFs (chaves de cruzamento WMS × SAP nem sempre são padronizadas)
- **Gestão da chave API:** Implementar carregamento seguro via `.env` sem expor credenciais no repositório

---

## 🔮 Próximos Passos

- [ ] Integrar janelas de recebimento futuras ao banco — o agente passará a informar não só o status dos recebimentos, mas a previsão de chegada do material conforme a necessidade do cliente
- [ ] Interface web simples para o cliente consultar sem precisar do terminal
- [ ] Histórico de consultas e log de respostas do agente

---

## 👤 Autor

**Gabriel Passos França**
Analista de Logística & Automação de Processos
[LinkedIn](https://linkedin.com/in/gabriel-franca-logistica) · [GitHub](https://github.com/logistic-machine)
