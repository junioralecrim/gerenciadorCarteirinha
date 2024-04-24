

-- Tabela para cadastro de alunos
CREATE TABLE Alunos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    CPF VARCHAR(14) UNIQUE NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    PlasticoCarteirinha VARCHAR(100) NOT NULL,
    Vigencia DATE NOT NULL,
    DataCadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabela para cadastro de universidades/escolas
CREATE TABLE Instituicoes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    EmailInstitucional VARCHAR(100) UNIQUE NOT NULL,
    Senha VARCHAR(255) NOT NULL, -- Deverá ser armazenado com hash
    DataCadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabela para solicitações de segunda via
CREATE TABLE SolicitacoesSegundaVia (
    id INT AUTO_INCREMENT PRIMARY KEY,
    AlunoID INT,
    Motivo VARCHAR(100) NOT NULL,
    Status ENUM('Pendente', 'Em Processo', 'Concluída') DEFAULT 'Pendente',
    DataSolicitacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AlunoID) REFERENCES Alunos(id)
);

-- Tabela para autenticação
CREATE TABLE Autenticacao (
    id INT AUTO_INCREMENT PRIMARY KEY,
    InstituicaoID INT,
    EmailInstitucional VARCHAR(100) NOT NULL,
    Senha VARCHAR(255) NOT NULL, -- Será armazenada de forma segura (hash)
    DataUltimoAcesso TIMESTAMP,
    FOREIGN KEY (InstituicaoID) REFERENCES Instituicoes(id)
);

-- Tabela para envio de comprovante de matrícula e estudo
CREATE TABLE Comprovantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    AlunoID INT,
    InstituicaoID INT,
    Ano INT NOT NULL,
    ComprovanteArquivo VARCHAR(255) NOT NULL,
    DataEnvio TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AlunoID) REFERENCES Alunos(id),
    FOREIGN KEY (InstituicaoID) REFERENCES Instituicoes(id)
);

-- Tabela para envio de documentação para segunda via
CREATE TABLE DocumentacaoSegundaVia (
    id INT AUTO_INCREMENT PRIMARY KEY,
    SolicitacaoID INT,
    DocumentoComprovacao VARCHAR(255) NOT NULL,
    BoletimOcorrenciaArquivo VARCHAR(255),
    DataEnvio TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (SolicitacaoID) REFERENCES SolicitacoesSegundaVia(id)
);

-- Tabela para armazenar solicitações de renovação
CREATE TABLE SolicitacoesRenovacao (
    id INT AUTO_INCREMENT PRIMARY KEY,
    AlunoID INT,
    AnexoRenovacao VARCHAR(255) NOT NULL,
    Status ENUM('Pendente', 'Em Processo', 'Concluída') DEFAULT 'Pendente',
    DataSolicitacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AlunoID) REFERENCES Alunos(id)
);

-- Tabela para armazenar solicitações de nova via
CREATE TABLE SolicitacoesNovaVia (
    id INT AUTO_INCREMENT PRIMARY KEY,
    AlunoID INT,
    AnexoRenovacao VARCHAR(255) NOT NULL,
    BoletimOcorrenciaArquivo VARCHAR(255) NOT NULL,
    Status ENUM('Pendente', 'Em Processo', 'Concluída') DEFAULT 'Pendente',
    DataSolicitacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AlunoID) REFERENCES Alunos(id)
);

-- Tabela para validação de documentos
CREATE TABLE ValidacaoDocumentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    UsuarioID INT,
    SolicitacaoID INT,
    DocumentosValidados BOOLEAN DEFAULT false,
    DataValidacao TIMESTAMP,
    FOREIGN KEY (UsuarioID) REFERENCES Autenticacao(id),
    FOREIGN KEY (SolicitacaoID) REFERENCES SolicitacoesNovaVia(id)
);

-- Tabela para órgãos públicos
CREATE TABLE OrgaosPublicos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    AutenticacaoID INT UNIQUE,
    DataCadastro TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AutenticacaoID) REFERENCES Autenticacao(id)
);

-- Tabela para documentos enviados
CREATE TABLE DocumentosEnviados (
    id INT AUTO_INCREMENT PRIMARY KEY,
    AlunoID INT,
    Documento VARCHAR(255) NOT NULL,
    DataEnvio TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AlunoID) REFERENCES Alunos(id)
);

-- Tabela de associação entre órgãos públicos e documentos
CREATE TABLE VisualizacaoDocumentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    OrgaoPublicoID INT,
    DocumentoEnviadoID INT,
    DataVisualizacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    Validado BOOLEAN DEFAULT false,
    FOREIGN KEY (OrgaoPublicoID) REFERENCES OrgaosPublicos(id),
    FOREIGN KEY (DocumentoEnviadoID) REFERENCES DocumentosEnviados(id)
);
