--1
SELECT nome_funcionario, nome_depto
FROM funcionario, departamento
WHERE nome_depto
LIKE '%Recursos Humanos%';
--2
select  distinct nome_funcionario
from funcionario
where codfuncionario in (
    select codfuncionario
    from projeto
    where sigla_depto in ('MKT', 'HR') 
);
--3
select nome_depto, (
select SUM(salario)
from funcionario
where sigla_depto = sigla_depto
) AS total_salario
from departamento;
--4
select nome_funcionario
from funcionario 
where sigla_depto = 'TI' and salario > (
select avg(salario)
from funcionario
where sigla_depto = 'TI'
);
-- 5. 
SELECT nome_depto, (
     SELECT COUNT(codfuncionario)
     FROM funcionario
     WHERE sigla_depto = sigla_depto
) AS qtdfuncionariosdepto
FROM departamento;
- 6.
SELECT nome_funcionario
FROM funcionario
WHERE sigla_depto = 'HR' 
AND salario > (SELECT AVG(salario) FROM funcionario WHERE sigla_depto = 'HR');

-- 7. 
SELECT nome_depto,
       (SELECT GROUP_CONCAT(nome_funcionario SEPARATOR ', ')
        FROM funcionario
        WHERE sigla_depto = d.sigla_depto) AS funcionarios
FROM departamento d;
