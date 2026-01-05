# trabalhobd
-- =========================================
-- DCL - SEGURANÇA DO BANCO DE DADOS
-- =========================================

-- 1. Criar usuários
CREATE USER 'admin_db'@'localhost' IDENTIFIED BY 'admin123';
CREATE USER 'usuario_leitura'@'localhost' IDENTIFIED BY 'leitura123';
CREATE USER 'usuario_operacao'@'localhost' IDENTIFIED BY 'operacao123';

-- 2. Conceder permissões

-- Admin: todas as permissões no banco
GRANT ALL PRIVILEGES ON escola_db.* TO 'admin_db'@'localhost';

-- Usuário apenas leitura
GRANT SELECT ON escola_db.* TO 'usuario_leitura'@'localhost';

-- Usuário de operação (DML)
GRANT SELECT, INSERT, UPDATE, DELETE ON escola_db.* TO 'usuario_operacao'@'localhost';

-- Aplicar alterações
FLUSH PRIVILEGES;

-- 3. Revogação de permissões (exemplo)

-- Revogar DELETE do usuário de operação
REVOKE DELETE ON escola_db.* FROM 'usuario_operacao'@'localhost';

-- Aplicar novamente
FLUSH PRIVILEGES;
