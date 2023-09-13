## Equipe: VIRUS


## Subgrupo: A  (BOYS)

- Lucas Gabriel Monteiro Da Costa - 183967 
- Pietro Grazzioli Golfeto - 223694 
- Vitor Rodrigues Zanata da Silva - 231718 

## Soluções (contidas no notebook Jupiter)

    Ex 1:
    select Food_Code, FCID_Code, Ingredient_Num, Commodity_Weight
    from Recipes
    where Food_Code = 27111300 and Mod_Code = 0;
    
    Ex 2:
    select R.Food_Code, R.FCID_Code, F.FCID_Desc, R.Ingredient_Num, R.Commodity_Weight
    from Recipes R, FCID_Description F
    where R.Food_Code = 27111300 and R.Mod_Code = 0 and R.FCID_Code = F.FCID_Code;
    
    Ex 3:
    select distinct C.CGN, C.Crop_Group_Description
    from Recipes R, FCID_Description F, Crop_Group C 
    where R.Food_Code = 27111300 and R.Mod_Code = 0 and R.FCID_Code = F.FCID_Code
    and F.CGN = C.CGN and C.CGN = C.CGL;
    
    Ex 4:
    select F.FCID_Desc, count(*)
    from Recipes R, FCID_Description F
    where R.FCID_Code = F.FCID_Code
    group by R.FCID_Code
    order by count(*) desc;
    
    Ex 5:
    select distinct C.Crop_Group_Description, avg(I.Intake) 
    from FCID_Description F, Crop_Group C, Intake I
    where F.CGN = C.CGN and C.CGN = C.CGL and F.FCID_Code = I.FCID_Code
    group by C.CGN
    order by avg(I.Intake) desc;


  
