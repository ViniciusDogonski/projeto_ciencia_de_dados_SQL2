
### Esquema Lógico do Banco de Dados para Oficina:

Tabelas:
- Cliente (cliente_id, nome, telefone)
- Carro (carro_id, cliente_id, marca, modelo)
- Servico (servico_id, descricao, valor)
- Carro_Servico (carro_id, servico_id, data)
- Funcionario (funcionario_id, nome, cargo)
- Atendimento (atendimento_id, carro_id, funcionario_id, data)

### Consultas SQL de Exemplo:

1. Recuperação simples de todos os carros:
```sql
SELECT * FROM Carro;
```

2. Filtro para mostrar carros de um cliente específico:
```sql
SELECT * FROM Carro WHERE cliente_id = 123;
```

3. Criação de uma coluna derivada que calcula o valor total gasto por cliente:
```sql
SELECT Cliente.nome, SUM(Servico.valor) AS valor_total_gasto
FROM Cliente
JOIN Carro ON Cliente.cliente_id = Carro.cliente_id
JOIN Carro_Servico ON Carro.carro_id = Carro_Servico.carro_id
JOIN Servico ON Carro_Servico.servico_id = Servico.servico_id
GROUP BY Cliente.nome;
```

4. Ordenar serviços por valor em ordem decrescente:
```sql
SELECT * FROM Servico ORDER BY valor DESC;
```

5. Mostrar a quantidade de atendimentos realizados por cada funcionário:
```sql
SELECT funcionario_id, COUNT(*) AS num_atendimentos
FROM Atendimento
GROUP BY funcionario_id;
```

6. Relação de carros e os serviços realizados neles:
```sql
SELECT Carro.modelo, Servico.descricao
FROM Carro
JOIN Carro_Servico ON Carro.carro_id = Carro_Servico.carro_id
JOIN Servico ON Carro_Servico.servico_id = Servico.servico_id;
```

7. Mostrar atendimentos com mais de 2 serviços:
```sql
SELECT Atendimento.atendimento_id, COUNT(*) AS num_servicos
FROM Atendimento
JOIN Carro_Servico ON Atendimento.carro_id = Carro_Servico.carro_id
GROUP BY Atendimento.atendimento_id
HAVING num_servicos > 2;
```
