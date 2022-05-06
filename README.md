# Separando Texto de Números
Essa query tem o objetivo de separar textos de números para tratativa de campos com os dois tipos de dados.

[Learn at Knowstar](https://www.youtube.com/watch?v=XAzkr3-Rfjg&t=903s)

				DECLARE @STRING AS VARCHAR(MAX) = '22November202022';

				WITH CHARACTER AS 
				(
					SELECT 
							STUFF(@STRING, 1, 1, '') AS REM_STR
						  , LEFT(@STRING, 1) AS COL
					UNION ALL
					(
					SELECT 
							STUFF(REM_STR, 1, 1, '') AS REM_STR
						  , LEFT(REM_STR, 1) AS COL
					FROM
						CHARACTER
					WHERE
						LEN(REM_STR) > 0
					)
				)

				-- DADOS LINHA A LINHA MOSTRANDO A DECOMPOSICAO DA STRING
				--SELECT 
				--		REM_STR
				--	  , COL
				--FROM
				--		CHARACTER
				--WHERE
				--		1=1
						--REM_STR LIKE '[0-9]'  -- SÓ NÚMERO
						-- REM_STR LIKE '[aA-zA]'  -- SÓ TEXTO

				-- AGREGANDO O TEXTO EM UMA SO LINHA
				SELECT
						STRING_AGG(REM_STR, '')
				FROM
						CHARACTER

