## Equipe: VIRUS


## Subgrupo: A  (BOYS)

- Lucas Gabriel Monteiro Da Costa - 183967 
- Pietro Grazzioli Golfeto - 223694 
- Vitor Rodrigues Zanata da Silva - 231718 

## Soluções

### Ex1:
  drop view numReceitas if exists;
  
  create view numReceitas as  
  select FCID_Code, count(distinct Food_Code) as num from Recipes group by FCID_Code
  
  drop view Metricas if exists;  
  create view Metricas as  
  
  select F.FCID_Code, F.FCID_Desc, F.CGN, F.CG_Subgroup,
  count(distinct I.seqn) as Popularidade, sum(I.Intake) as Intake_Sum,
  sum(I.Intake)/count(distinct I.seqn) as Intake_AVG,
  sum(I.Intake_BW)/count(distinct I.seqn) as Intake_AVG_BW,
  N.num as Recipes
  
  from FCID_Description F, Intake I, numReceitas N  
  where F.FCID_Code = I.FCID_Code and F.FCID_Code = N.FCID_Code  
  group by I.FCID_Code

### Ex2:
  --Top 25 mais consumidos em quantidade  
  drop view Qtd if exists;
  create view Qtd as select * from Metricas order by Intake_sum desc limit 25

  --Top 25 mais consumidos em numero de pessoas  
  drop view Pop if exists;
  create view Pop as select * from Metricas order by Popularidade desc limit 25

  --Relação entre os dois
  select Q.FCID_Code, Q.FCID_Desc, Q.Popularidade, Q.Intake_Sum, Q.Intake_AVG, Q.Intake_AVG_BW, Q.Recipes  
  from Qtd Q, Pop P where Q.FCID_Code = P.FCID_Code

### Ex3:
  -- Classe de alimento mais consumido por consumidor  
  drop view Cons if exists;
  
  create view Cons as    
  select I.seqn, F.CGN
  
  from Intake I, FCID_Description F
  
  where I.FCID_Code = F.FCID_Code
  and F.CGN = (select top(1) CGN from Intake J, FCID_Description G
               where J.FCID_Code = G.FCID_Code and J.seqn = I.seqn
               group by G.CGN
               order by sum(J.Intake) desc
              )


### Ex4:
  Deve-se considerar as seguintes métricas:

* Alimentos mais consumidos por cada consumidor permitindo comparar as preferencias alimentares de cada perfil.  
* Categoria de consumo de cada consumidor, classificado em vegano, vegetariano e carnívoro  
* Indicador de nutrição, desnutrição e saúde a partir de uma avaliação do consumo em gramas médio por peso corporal de cada pessoa.

-- Alimento mais consumido por pessoa  
drop view Cons if exists;  
create view Cons as

select I.seqn, F.CGN

from Intake I, FCID_Description F

where I.FCID_Code = F.FCID_Code  
and F.CGN = (select top(1) J.FCID_Code from Intake J
             where and J.seqn = I.seqn
             group by J.FCID_Code
             order by sum(J.Intake) desc
            )
