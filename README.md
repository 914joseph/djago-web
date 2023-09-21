# djago-web

from django.db import models

class Alunos(models.Model):
    id_aluno = models.AutoField(primary_key=True)
    nome = models.CharField(max_length=255)
    cpf = models.CharField(max_length=11)
    rg = models.CharField(max_length=8)
    matricula = models.CharField(max_length=5)
    telefone = models.CharField(max_length=11)
    email = models.CharField(max_length=255)

class Professores(models.Model):
    id_professor = models.AutoField(primary_key=True)
    nome = models.CharField(max_length=255)
    cpf = models.CharField(max_length=11)
    rg = models.CharField(max_length=8)
    codigo = models.CharField(max_length=8)
    email = models.CharField(max_length=255)
    telefone = models.CharField(max_length=11)

class Disciplinas(models.Model):
    id_disciplina = models.AutoField(primary_key=True)
    id_professor = models.ForeignKey(Professores, on_delete=models.CASCADE)
    nome = models.CharField(max_length=255)
    codigo = models.CharField(max_length=7)
    carga_horaria = models.IntegerField()
    ementa = models.TextField(null=True,blank=True)

class DisciplinaAluno(models.Model):
    id_matricula = models.AutoField(primary_key=True)
    id_aluno = models.ForeignKey(Alunos, on_delete=models.CASCADE)
    id_disciplina = models.ForeignKey(Disciplinas, on_delete=models.CASCADE)
    nota = models.FloatField(null=True,blank=True)

class PlanoAula(models.Model):
    id_plano_aula = models.AutoField(primary_key=True)
    id_disciplina = models.ForeignKey(Disciplinas, on_delete=models.CASCADE)
    tema_aula = models.CharField(max_length=255)
    conteudo = models.TextField()
    metodo = models.CharField(max_length=50)
    dia = models.DateTimeField()

class Frequencia(models.Model):
    id_frequencia = models.AutoField(primary_key=True)
    id_materia = models.ForeignKey(Disciplinas, on_delete=models.CASCADE)
    dia = models.DateTimeField()

class FrequenciaAluno(models.Model):
    id = models.AutoField(primary_key=True)
    id_aluno = models.ForeignKey(Alunos, on_delete=models.CASCADE)
    id_frequencia = models.ForeignKey(Frequencia, on_delete=models.CASCADE)
    presenca = models.BooleanField()


class Atividades(models.Model):
    id_atividade = models.AutoField(primary_key=True)
    atividade = models.TextField()
    tipo = models.CharField(max_length=50)
    data_postagem = models.DateTimeField(auto_now_add=True)
    data_entrega = models.DateTimeField(auto_now_add=True,null=True,blank=True)
    id_desciplina = models.ForeignKey(Disciplinas, on_delete=models.CASCADE)
    id_plano_aula = models.ForeignKey(PlanoAula, on_delete=models.CASCADE)


class AtividadeAluno(models.Model):
    id = models.AutoField(primary_key=True)
    id_atividade = models.ForeignKey(Atividades, on_delete=models.CASCADE)
    id_aluno = models.ForeignKey(Alunos, on_delete=models.CASCADE)
    nota = models.FloatField(null=True,blank=True)

