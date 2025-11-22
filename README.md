# 🗄️ Projeto de Banco de Dados - Rede de Hotéis & Locadora de Veículos

Este repositório contém o trabalho desenvolvido na disciplina de **Banco de Dados** do curso de **Ciência de Dados (UNINTER)**.  
O projeto aborda duas etapas principais: **modelagem conceitual (MER)** para uma rede de hotéis e **implementação lógica (SQL)** para uma locadora de veículos.

---

## 📌 1ª Etapa - Modelagem (Rede de Hotéis)

Foi elaborado um **Modelo Entidade-Relacionamento (MER)** contemplando:

- **Entidades**: Funcionário, Hotel, Quarto, Hóspede, Reserva, Pagamento  
- **Atributos**: CPF, nome, telefone, e-mail, login, senha, endereço, categoria, preço da diária, status etc.  
- **Relacionamentos**:
  - Um hotel possui vários quartos
  - Um funcionário realiza várias reservas
  - Um hóspede pode fazer várias reservas
  - Uma reserva gera um pagamento
- **Cardinalidades**: Definidas conforme regras de negócio
- **Chaves primárias e estrangeiras**: Representadas em cada entidade

📊 O MER garante a integridade dos dados e reflete fielmente as regras de negócio fornecidas.

---

## 📌 2ª Etapa - Implementação (Locadora de Veículos)

Foi criado um banco de dados chamado **`LocadoraVeiculos`** no MySQL Workbench, com as seguintes tabelas:

- **Cliente**  
- **Veículo**  
- **Manutenção**  
- **Pagamento**  
- **Locação**  
- **LocacaoVeiculo** (tabela associativa)

Todos os campos foram definidos como **NOT NULL**, respeitando chaves primárias e estrangeiras.

---

## 📊 Consultas SQL Implementadas

1. **Listar manutenções realizadas nos veículos**  
   ```sql
   select descricao, dataManutencao, custo from Manutencao;
   ```
2. **Valor total arrecadado pela locadora (somente pagos)**
  ```sql
  select sum(valorTotal) as ValorTotalArrecadado
  from Pagamento
  where estado = 'Pago';
  ```
3. **Modelos e marcas dos veículos com número de locações (ordem decrescente)**
   ```sql
   select v.modelo as Modelo,
       v.marca as Marca,
       COUNT(lv.idVeiculo) as NumeroDeLocacoes
       from Veiculo v
       inner join LocacaoVeiculo lv on v.idVeiculo = lv.idVeiculo
       group by v.modelo, v.marca
       order by NumeroDeLocacoes desc;
   ```
4.**Clientes com pagamentos pendentes e valores devidos (ordem alfabética)**
  ```sql
  select c.nome as NomeCliente,
       SUM(p.valorTotal) as ValorDevido
        from Cliente c
        inner join Locacao l on c.idCliente = l.idCliente
        inner join Pagamento p on l.idPagamento = p.idPagamento
        where p.estado = 'Pendente'
        group by c.nome
        order by c.nome asc;
```
## ✅ Resultados
- MER construído conforme regras de negócio da rede de hotéis.  
- Banco de dados **LocadoraVeiculos** implementado com sucesso.  
- Consultas SQL retornando resultados corretos (manutenções, arrecadação, locações e clientes devedores).  

---

## 🤝 Contribuição
Sugestões de melhorias são bem-vindas!  
Abra uma issue ou envie um pull request para colaborar.
