<div align="center">
  <h1>Destacando o Melhor e o Pior Mês no Power BI</h1>
</div>

<img width="1361" height="676" alt="Captura de tela 2026-01-12 200221" src="https://github.com/user-attachments/assets/811c14b8-67c7-46d0-ba6e-74ce3f919daf" />

<h2>Medida base</h2>

```DAX
Quantidade Vendida = SUM(fVendas[Quantidade])
```

<h2>Melhor Mês</h2>

```DAX
Maior_Mes_Quantidade_Vendida = 
VAR _MaiorValor = 
MAXX(
    ALLSELECTED('dCalendario'[Mes_Abreviado], dCalendario[Mes_Numero]),
    [Quantidade Vendida]
)
RETURN
IF(
    [Quantidade Vendida] = _MaiorValor,
    [Quantidade Vendida],
    BLANK()
)
```

<h2>Pior Mês</h2>

```DAX
Menor_Mes_Quantidade_Vendida = 
VAR _MenorValor = 
MINX(
    ALLSELECTED('dCalendario'[Mes_Abreviado], dCalendario[Mes_Numero]),
    [Quantidade Vendida]
)
RETURN
IF(
    [Quantidade Vendida] = _MenorValor,
    [Quantidade Vendida],
    BLANK()
)
```

<h2>Quantidade Vendida – Ano Anterior</h2>

```DAX
Quantidade Vendida LY = 
CALCULATE(
    [Quantidade Vendida],
    SAMEPERIODLASTYEAR(dCalendario[Date])
)
```

<h2>Configuração do gráfico</h2>

<img width="252" height="209" alt="image" src="https://github.com/user-attachments/assets/4bf82404-8951-4a70-a204-61a74473f6e3" />

<img width="252" height="589" alt="image" src="https://github.com/user-attachments/assets/95cf1dc3-c0f6-447b-ab23-33b08527c958" />

<img width="252" height="623" alt="image" src="https://github.com/user-attachments/assets/0984802d-7364-4c4b-b301-11b206628cb0" />





<h2>⭐ Suporte</h2>

Gostou do material? Não esqueça de deixar uma **estrela** ⭐ no repositório!

Se quiser incentivar a criação de mais conteúdos gratuitos, você pode contribuir por aqui:
[💙 Clique para Apoiar o Projeto](https://nubank.com.br/cobrar/15oae1/695e72ce-de11-494f-9405-f7c3a3466ac0)
