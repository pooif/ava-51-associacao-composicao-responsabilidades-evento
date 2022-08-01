# 5.1 // Associação, Composição e Responsabilidade // Atividade

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <https://classroom.github.com/a/czTlYTzW>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** associações, composição, atribuição de responsabilidades, coesão.

---

Implementar Sistema Eventos/Atividades conforme os Casos de Teste a seguir:

```java
// Eventos tem um nome, cidade, tipo e ano.
// Evento.Tipo é um enum público declarado dentro da classe Evento.
Evento ev1 = new Evento("Semana Acadêmica IFRS", "Rio Grande", Evento.Tipo.Semana, 2021);

// Todas as atividades tem vagas e a carga horária é opcional
// Atividade.Tipo é um enum público declarado dentro da classe Atividade.
Atividade atv1 = ev1.novaAtividade("Seminário TCCs TADS", 40, Atividade.Tipo.Seminario);
Atividade atv2 = ev1.novaAtividade("Minicurso ECMA6", 20, 8, Atividade.Tipo.Minicurso);
// Não deve ser possível instanciar a atividade a partir do App.java
// Atividade at = new Atividade("Seminário TCCs TADS", 40, Atividade.Tipo.Seminario);

// Dados do evento:
System.out.println(ev1.getNome().equals("Semana Acadêmica IFRS"));
System.out.println(ev1.getTipo() == Evento.Tipo.Semana);
System.out.println(ev1.getCidade().equals("Rio Grande"));
System.out.println(ev1.getAno() == 2021);

// Evento tem atividades: (não esqueça do import java.util.ArrayList;)
ArrayList<Atividade> atvs = ev1.getAtividades();
System.out.println(atvs.size() == 2);
System.out.println(atvs.get(0).equals(atv1));
System.out.println(atvs.get(1).equals(atv2));

// Método para obter atividades pela ordem de inserção, não é o index:
System.out.println(ev1.getAtividade(1).equals(atv1)); // 1ra atividade
System.out.println(ev1.getAtividade(2).equals(atv2)); // 2da atividade

// Dados das atividades:
System.out.println(atv1.getDescricao().equals("Seminário TCCs TADS"));
System.out.println(atv1.getVagas() == 40);
System.out.println(atv1.getTipo()  == Atividade.Tipo.Seminario);
System.out.println(atv1.getAno()   == 2021); // mesmo ano do evento

// Os minicursos têm carga horária:
System.out.println(atv2.getDescricao().equals("Minicurso ECMA6"));
System.out.println(atv2.getVagas() == 20);
System.out.println(atv2.getHoras() == 8);
System.out.println(atv2.getTipo()  == Atividade.Tipo.Minicurso);

// Todas as atividades pertencem a um evento: // Bidirecionalidade
System.out.println(atv1.getEvento().equals(ev1));
System.out.println(atv2.getEvento().equals(ev1));

// Ministrante tem nome e bio:
Ministrante paulo = new Ministrante("Paulo Silva", "Paulo é formado em Análise e Desenvolvimento de Sistemas pelo IFRS e possui 5 anos de experiência na área");
Ministrante maria = new Ministrante("Maria Santos", "Maria possui doutorado em Ciência de Dados e é professora na UFRGS há 8 anos");

// Outros tipo de eventos e atividades:
Evento ev2 = new Evento("Escola Regional de Banco de Dados", "Bagé", Evento.Tipo.Escola, 2021);
Atividade atv3 = ev2.novaAtividade("BigData com Apache Hadoop", paulo, 20, 4, Atividade.Tipo.Oficina);
Atividade atv4 = ev2.novaAtividade("Data Science: uma introdução", maria, Atividade.Tipo.Palestra);
Atividade atv5 = ev2.novaAtividade("Apache Kafka", maria, Atividade.Tipo.Palestra);

// Dados da atividade:
System.out.println(atv3.getDescricao().equals("BigData com Apache Hadoop"));
System.out.println(atv3.getMinistrante().equals(paulo));
System.out.println(atv3.getVagas() == 20);
System.out.println(atv3.getHoras() == 4);
System.out.println(atv3.getTipo()  == Atividade.Tipo.Oficina);
System.out.println(atv3.getAno()   == 2021);

// Um evento que abriga (tem) outros eventos:
Evento ev3 = new Evento("3º Salão de Pesquisa, Extensão e Ensino do IFRS", "Bento Gonçalves", Evento.Tipo.Salao, 2022);
EventoSatelite sat1 = ev3.novoEventoSatelite("7º Seminário de Iniciação Científica e Tecnológica (SICT)", Evento.Tipo.Seminario);
EventoSatelite sat2 = ev3.novoEventoSatelite("5º Seminário de Educação Profissional e Tecnológica (SEMEPT)", Evento.Tipo.Seminario);
EventoSatelite sat3 = ev3.novoEventoSatelite("Mostra de Arte e Cultura", Evento.Tipo.Mostra);

// Eventos satélites são da mesma cidade do evento central:
System.out.println(ev3.getCidade().equals("Bento Gonçalves"));
System.out.println(sat1.getCidade().equals(ev3.getCidade()));
System.out.println(sat1.getCidade().equals("Bento Gonçalves"));

// Eventos satélites pertencem a um evento central:
System.out.println(sat1.getEventoCentral().equals(ev3));

// Os eventos satélites:
System.out.println(ev3.getEventosSatelites().size() == 3);
System.out.println(ev3.getEventoSatelite(1).equals(sat1));
System.out.println(ev3.getEventoSatelite(2).equals(sat2));
System.out.println(ev3.getEventoSatelite(3).equals(sat3));

// Inscrição nas atividades:
System.out.println(atv1.getVagas() == 40);
System.out.println(atv1.getVagasRemanescentes() == 40);

// A inscrição parte de uma atividade, com o nome do inscrito:
Inscrito insc1 = atv1.inscrever("Jean-Luc Picard");
Inscrito insc2 = atv1.inscrever("Worf");

// Consultando o nome a partir de getNome e toString:
System.out.println(insc1.getNome().equals("Jean-Luc Picard"));
System.out.println(insc2.toString().equals("Worf"));

// As vagas decrescem:
System.out.println(atv1.getVagasRemanescentes() == 38); // 40 - 2 inscritos = 38 vagas

// A inscrição tem uma chave no formato AAAAAAAAAAAAAAAA até ZZZZZZZZZZZZZZZZ
// aleatória, como: AGGASCFFEERERRER  Importante: ela é gerada na inscrição
System.out.println(insc1.getChave()); // imprime a chave
// Verificando se a chave está de acordo com os requisitos:
Chave chave = insc1.getChave();
String chaveString = chave.toString();
System.out.println(chaveString.length() == 16); // tamanho 16
// Todos os 16 caracteres entre A a Z:
for (var c : chaveString.toCharArray()) System.out.println(c >= 65 && c <= 90); // A a Z

// As chaves não podem ser as mesmas, cada inscrito deve ter uma chave única:
System.out.println(insc1.getChave().equals(insc2.getChave()) == false);

// Por padrão cada inscrito não concluiu a atividade:
System.out.println(insc1.isConcluido() == false); // foi ao evento/atividade?

// A atividade tem inscritos
ArrayList<Inscrito> inscritos = atv1.getInscritos();
System.out.println(inscritos.get(0).equals(insc1));
System.out.println(inscritos.get(1).equals(insc2));
System.out.println(atv1.getInscrito(2).isConcluido() == false); // 2do inscrito

System.out.println(insc1.isConcluido() == false);
// Que confirmam presença (chamada)
insc1.confirmarPresenca(); // marcar como concluído
System.out.println(insc1.isConcluido() == true);
System.out.println(atv1.getInscrito(1).isConcluido() == true);
System.out.println(atv1.getInscrito(2).isConcluido() == false);
atv1.getInscrito(2).confirmarPresenca();
System.out.println(atv1.getInscrito(2).isConcluido() == true);

// Inscrevendo 38 klingons no evento #1
for (int i = 0; i < 38; i++) atv1.inscrever("Klingon #" + i);

// A atividade sem vagas abertas:
System.out.println(atv1.getVagasRemanescentes() == 0);

// Logo, não é possível inscrever-se mais:
try {
  atv1.inscrever("Data");
  System.out.println(false); // esta linha não deve ser executada
} catch (NaoHaVagaException e) { // criar esta classe NaoHaVagaException extends Exception
  System.err.println(true + " " + e); // Não há mais vagas!
}

// Eventos satélite permitem inscrição como os outros eventos
sat1.inscrever("Geordi Laforge");

// Eles não tem limite de inscritos
// e tem todas as propriedades que um inscrito tem nas atividades
System.out.println(sat1.getInscrito(1).getNome().equals("Geordi Laforge"));
Inscrito insc3 = sat1.getInscrito(1);
Chave chave3 = insc3.getChave();
System.out.println(insc3 != null);
System.out.println(chave3 != null);
System.out.println(chave3); // Uma chave de 16 caracteres entre A e Z
System.out.println(sat1.getQuantidadeInscritos() == 1);
// esta atividade não tem limite de vagas nem carga horária
System.out.println(atv4.getVagas() == 0);
System.out.println(atv4.getHoras() == 0);
System.out.println(atv4.getVagasRemanescentes() == 0);
System.out.println(atv4.getTipo().equals(Atividade.Tipo.Palestra));
// então não há limite de inscrições
atv4.inscrever("Beverly Crusher");
atv4.inscrever("Deanna Troi");
System.out.println(atv4.getInscritos().size() == 2);
System.out.println(atv4.getQuantidadeInscritos() == 2);
```
```

---
Obs.: os casos de teste não podem ser alterados, mas outros podem ser adicionados. Fique a vontade para adicionar códigos que imprimem ou separam os testes, por exemplo.
