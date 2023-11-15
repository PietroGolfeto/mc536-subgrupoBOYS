## Equipe: VIRUS


## Subgrupo: A  (BOYS)

- Lucas Gabriel Monteiro Da Costa - 183967 
- Pietro Grazzioli Golfeto - 223694 
- Vitor Rodrigues Zanata da Silva - 231718 


## Soluções

### Ex1:


### Ex2:
    // Iniciaizando Drug e Pathology
    LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug.csv' AS line
    CREATE (:Drug {code: line.code, name: line.name})

    CREATE INDEX for (d:Drug) ON (d.code)

    LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/pathology.csv' AS line
    CREATE (:Pathology { code: line.code, name: line.name})

    CREATE INDEX for (p:Pathology) ON (p.code)

    // Drug use CSV
    LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS line
    CREATE (:DrugUse {idperson: line.idperson, codepathology: line.codepathology, codedrug: line.codedrug})

    CREATE INDEX FOR (du: DrugUse) ON (du.idperson)

    // Side effect CSV
    LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS line
    CREATE (:SideEffect {idperson: line.idPerson, codepathology: line.codePathology})

    CREATE INDEX FOR (se: SideEffect) ON (se.idperson)

    // Relacionando drogas e seus side effects
    MATCH (s:SideEffect)
    MATCH (p:DrugUse)
    match(pat:Pathology {code: s.codepathology})
    match(dr:Drug {code: p.codedrug})
    WHERE s.idperson = p.idperson
    MERGE (dr)-[t:HasSideEffect]->(pat)
    ON CREATE SET t.weight=1
    ON MATCH SET t.weight=t.weight+1

    // Visualizando
    match (dr:Drug)-[t:HasSideEffect]->(pat:Pathology)
    where t.weight > 10
    return dr, t, pat

### Ex3: 
