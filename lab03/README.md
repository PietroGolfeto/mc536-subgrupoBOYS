## Equipe: VIRUS


## Subgrupo: A  (BOYS)

- Lucas Gabriel Monteiro Da Costa - 183967 
- Pietro Grazzioli Golfeto - 223694 
- Vitor Rodrigues Zanata da Silva - 231718 

## Modelo relacional dos diagramas do lab02

CARDAPIO_DIARIO(_data_, cafe, almoco, janta)
    cafe chave estrangeira -> REFEICAO(id)
    almoco chave estrangeira -> REFEICAO(id)
    janta chave estrangeira -> REFEICAO(id)
    
REFEICAO(_id_, turno, refData)
    refData chave estrangeira -> CARDAPIO_DIARIO

PORCAO(_id_, nome, categoria, descricao)

// relaciona refeicao e porcoes que a compoem
PORCOES_POR_REFEICAO(_idRefeicao_, _idPorcao_)
    idRefeicao chave estrangeira -> REFEICAO(id)
    idPorcao chave estrangeira -> PORCAO(id)

INGREDIENTE(_id_, nome, idNutri)
    idNutri chave estrangeira -> NUTRIENTES(id)

INGREDIENTE_POR_PORCAO(_idPorcao_, _idIngrediente_)
    idPorcao chave estrangeira -> PORCAO(id)
    idIngrediente chave estrangeira -> INGREDIENTE(id)

NUTRIENTES(_id_, carboidratos, proteinas, lipideos, fibras, sodio)

//relaciona ingrediente e sua composicao por outros ingredientes
COMPOSICAO_INGREDIENTE(_idIngrediente_, _idSuperIngrediente_)
    idIngrediente chave estrangeira -> INGREDIENTE(id)
    idSuperIngrediente chave estrangeira -> INGREDIENTE(id)

ALUNO(_ra_, nome)

REFEICAO_ALUNO(_id_, idRefeicaoPrincipal, raAluno, idPorcaoBase, idPorcaoPrincipal, idPorcaoSalada, idPorcaoSobremesa)
    idRefeicaoPrincipal chave estrangeira -> REFEICAO(id)
    raAluno chave estrangeira -> ALUNO(ra)
    idPorcaoBase chave estrangeira -> PORCAO(id)
    idPorcaoPrincipal chave estrangeira -> PORCAO(id)
    idPorcaoSalada chave estrangeira -> PORCAO(id)
    idPorcaoSobremesa chave estrangeira -> PORCAO(id)
