<template>
  <transition
    appear
    enter-active-class="animated zoomIn"
    leave-active-class="animated zoomOut"
  >
    <q-page class="flex flex-center fundo">
      <div id="documento" class="shadow-box shadow-up-10">
        <q-page-sticky position="bottom-right" :offset="[250, 200]">
          <q-btn fab icon="edit_note" color="green" @click="prompt = true" />
        </q-page-sticky>
        <q-page-sticky position="bottom-right" :offset="[250, 130]">
<<<<<<< HEAD
          <q-btn fab icon="print" color="primary" @click="imprimir()" />
        </q-page-sticky>
        <q-page-sticky position="bottom-right" :offset="[250, 60]">
=======
>>>>>>> 7e335c3dd0c77896cd9d5ccc641bb282978dc30d
          <q-btn fab icon="picture_as_pdf" color="accent" @click="makepdf()" />
        </q-page-sticky>
        <q-page-sticky position="bottom-right" :offset="[250, 60]">
          <q-btn fab icon="print" color="primary" @click="imprimir()" />
        </q-page-sticky>
        <q-dialog v-model="prompt">
          <q-card style="min-width: 600px">
            <q-form @submit.prevent @reset="onReset" class="q-gutter-md">
              <q-card-section>
                <div class="text-h6">Preencha as Informações</div>
              </q-card-section>

              <q-card-section class="q-pt-none">
                <q-input
                  class="q-mb-md"
                  clearable
                  clear-icon="close"
                  filled
                  dense
                  v-model="this.form.nome"
                  label="Digite o nome a quem vai emprestar"
                  hint="Nome e sobrenome"
                  lazy-rules
                  :rules="[
                    (val) =>
                      (val && val.length > 0) || 'É necessário digitar o nome',
                  ]"
                >
                  <template v-slot:append>
                    <q-icon name="person" />
                  </template>
                </q-input>
                <div class="row">
                  <q-input
                    v-if="this.cpf"
                    class="q-mb-md col-8"
                    clearable
                    clear-icon="close"
                    filled
                    @keyup="verificarCPF(cpf)"
                    dense
                    type="text"
                    v-model="this.form.siapecpf"
                    label="CPF"
                    hint="Digite o CPF"
                    mask="###.###.###-##"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val !== null && val !== '') ||
                        'Por favor digite o CPF',
                      this.cpfFalso || 'Insira um SIAPE válido',
                    ]"
                  >
                    <template v-slot:append>
                      <q-icon name="remember_me" />
                    </template>
                  </q-input>
                  <q-input
                    v-else
                    class="q-mb-md col-8"
                    clearable
                    clear-icon="close"
                    filled
                    dense
                    type="text"
                    v-model="this.form.siapecpf"
                    label="SIAPE"
                    hint="Digite o SIAPE"
                    mask="########"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val !== null && val !== '') ||
                        'Por favor digite o Siape',
                      (val) => val.length <= 8 || 'Insira um SIAPE válido',
                    ]"
                  >
                    <template v-slot:append>
                      <q-icon name="badge" />
                    </template>
                  </q-input>
                  <q-toggle
                    v-model="this.cpf"
                    class="col self-start"
                    left-label
                    size="lg"
                    color="green"
                    icon="person"
                    label="CPF?"
                  />
                </div>
                <div class="row">
                  <q-input
                    v-if="this.cel"
                    class="q-mb-md col-8"
                    clearable
                    clear-icon="close"
                    filled
                    dense
                    v-model="this.form.tel"
                    label="Digite o Celular"
                    hint="Celular com ddd"
                    mask="(##) ##### - ####"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'É necessário digitar o celular de contato',
                    ]"
                  >
                    <template v-slot:append>
                      <q-icon name="phone_iphone" />
                    </template>
                  </q-input>
                  <q-input
                    v-else
                    class="q-mb-md col-8"
                    clearable
                    clear-icon="close"
                    filled
                    dense
                    v-model="this.form.tel"
                    label="Digite o Telefone"
                    hint="Telefone com ddd"
                    mask="(##) #### - ####"
                    lazy-rules
                    :rules="[
                      (val) =>
                        (val && val.length > 0) ||
                        'É necessário digitar o telefone de contato',
                    ]"
                  >
                    <template v-slot:append>
                      <q-icon name="call" />
                    </template>
                  </q-input>
                  <q-toggle
                    v-model="this.cel"
                    class="col self-start"
                    left-label
                    size="lg"
                    color="blue"
                    icon="phone_iphone"
                    label="Celular?"
                  />
                </div>
                <q-input
                  class="q-mb-md"
                  clearable
                  clear-icon="close"
                  filled
                  dense
                  v-model="this.form.origem"
                  label="Setor ou Unidade de Origem:"
                  hint="Digite o setor ou unidade ao qual pertence o equipamento"
                  lazy-rules
                  :rules="[
                    (val) =>
                      (val && val.length > 0) ||
                      'É necessário digitar o setor de origem',
                  ]"
                >
                  <template v-slot:append>
                    <q-icon name="move_up" />
                  </template>
                </q-input>
                <q-input
                  class="q-mb-md"
                  clearable
                  clear-icon="close"
                  filled
                  dense
                  v-model="this.form.setor"
                  label="Setor ou Unidade de Destino:"
                  hint="Digite o setor ou unidade ao qual ficará o equipamento"
                  lazy-rules
                  :rules="[
                    (val) =>
                      (val && val.length > 0) ||
                      'É necessário digitar o setor de destino',
                  ]"
                  ><template v-slot:append>
                    <q-icon name="move_down" />
                  </template>
                </q-input>
                <q-input
                  clearable
                  clear-icon="close"
                  v-model="this.form.equipamento"
                  filled
                  dense
                  label="Descrição do equipamento:"
                  type="textarea"
                  hint="Digite a especificação, marca, tombo etc do equipamento"
                  lazy-rules
                  :rules="[
                    (val) =>
                      (val && val.length > 0) ||
                      'É necessário digitar a especificação do equipamento',
                  ]"
                >
                  <template v-slot:append>
                    <q-icon name="weekend" />
                  </template>
                </q-input>
              </q-card-section>

              <q-card-actions align="right" class="text-primary">
                <q-btn
                  label="Limpar"
                  type="reset"
                  color="primary"
                  @click="limpar()"
                  flat
                  class="q-ml-sm"
                />
                <q-btn label="Cancelar" color="negative" v-close-popup />
                <q-btn
                  label="Preencher"
                  type="submit"
                  color="primary"
                  v-close-popup
                />
              </q-card-actions>
            </q-form>
          </q-card>
        </q-dialog>
        <div class="principal">
          <table>
            <tr>
              <td>
                <img class="imgufba" alt="ufba logo" src="../assets/UFBA.jpg" />
              </td>
              <td class="titulo">
                <span>{{ this.titulo }}</span
                ><br /><span class="unidade">{{ this.subtitulo }}</span>
              </td>
              <td>
                <img alt="faced logo" src="../assets/faced.png" />
              </td>
            </tr>
          </table>
          <h3 class="h3">Termo de Empréstimo de Equipamentos</h3>
          <table class="dados">
            <tr>
              <td>Nome: {{ this.form.nome }}</td>
            </tr>
            <tr>
              <td>Siape/CPF: {{ this.form.siapecpf }}</td>
            </tr>
            <tr>
              <td>Tel. para Contato: {{ this.form.tel }}</td>
            </tr>
            <tr>
              <td>Setor/Unidade: {{ this.form.setor }}</td>
            </tr>
            <tr>
              <td>Especificação do Equipamento: {{ this.form.equipamento }}</td>
            </tr>
          </table>
          <br />
          <div class="responsabilidade">
            <p>
              Pelo presente Termo de Entrega e Responsabilidade, o servidor
              acima qualificado declara que recebeu o equipamentos e acessórios
              acima especificados, de propriedade do setor/unidade:
              {{ this.form.origem }}, assumindo o compromisso de manter a guarda
              pessoal sobre os mesmos, ficando a seu cargo:
            </p>
            <ul>
              <li>Adequada utilização, de acordo com as recomendações;</li>
              <li>
                Comprometer-se a não conceder empréstimo ou confiar a outrem;
              </li>
              <li>
                Comunicar imediatamente qualquer incidente e ocorrência com o
                equipamento sob sua guarda e responsabilidade;
              </li>
              <li>
                Indenizar os danos causados por negligência, imprudência,
                imperícia, <br />má utilização, guarda inadequada, desleixo ou
                outro dano que possa decorrer, direta ou indiretamente, de sua
                ação ou omissão.
              </li>
            </ul>
          </div>
          <div class="assinatura">
            <br />
            <span>Salvador, </span>{{ dataAtual }} <br /><br /><br />
            <span> Assinatura: </span>
            <span>________________________________________</span>
          </div>
        </div>
      </div>
    </q-page>
  </transition>
</template>

<style>
</style>

<script>
import html2canvas from "html2canvas";
import jspdf from "jspdf";
import { ref } from "vue";

export default {
  name: "DocumentoPDF",
  data() {
    return {
      titulo: "Universidade Federal da Bahia",
      subtitulo: "Faculdade de Educação",
      cel: false,
      cpf: false,
      cpfFalso: false,
      form: {
        nome: "",
        tel: "",
        setor: "",
        siapecpf: "",
        equipamento: "",
        origem: "",
      },
    };
  },
  computed: {
    dataAtual() {
      let hoje = new Date();
      let data_formatada = hoje.toLocaleDateString("pt-BR", {
        day: "numeric",
        month: "long",
        year: "numeric",
      });
      return data_formatada;
    },
  },
  setup() {
    return {
      prompt: ref(false),
    };
  },
  watch: {
    cel(novo) {
      if (novo) {
        this.form.tel = "";
      } else {
        this.form.tel = "";
      }
    },
    cpf(novo) {
      if (novo) {
        this.form.siapecpf = "";
      } else {
        this.form.siapecpf = "";
      }
    },
  },
  methods: {
<<<<<<< HEAD
=======
    verificarCPF(cpf) {
      let strCPF = cpf.replace("-", "").replace(".", "");
      let Soma;
      let Resto;
      Soma = 0;
      if (strCPF == "00000000000") return false;

      for (i = 1; i <= 9; i++)
        Soma = Soma + parseInt(strCPF.substring(i - 1, i)) * (11 - i);
      Resto = (Soma * 10) % 11;

      if (Resto == 10 || Resto == 11) Resto = 0;
      if (Resto != parseInt(strCPF.substring(9, 10))) return false;

      Soma = 0;
      for (i = 1; i <= 10; i++)
        Soma = Soma + parseInt(strCPF.substring(i - 1, i)) * (12 - i);
      Resto = (Soma * 10) % 11;

      if (Resto == 10 || Resto == 11) Resto = 0;
      if (Resto != parseInt(strCPF.substring(10, 11))) return false;
      return true;
    },
>>>>>>> 7e335c3dd0c77896cd9d5ccc641bb282978dc30d
    imprimir() {
      window.print();
    },
    limpar() {
      this.form = {
        nome: "",
        tel: "",
        setor: "",
        siapecpf: "",
        equipamento: "",
        origem: "",
      };
    },
    makepdf() {
      window.html2canvas = html2canvas;
      let doc = new jspdf("p", "pt", "a4");
      doc.html(document.querySelector("#documento"), {
        callback: function (pdf) {
          pdf.save("TermoResponsabilidade.pdf");
          alert(
            "Documento Gerado com Sucesso!!! Escolha a pasta para salvar o documento"
          );
        },
      });
    },
  },
};
</script>

<style scoped>
.fundo {
  background-color: darkgray;
  padding: 3%;
}
#documento {
  font-family: Arial, Helvetica, sans-serif;
  padding-top: 30px;
  height: 8.4in;
  width: 6.2in;
  background-color: white;
}
img {
  width: 70px;
  height: 45px;
  margin: 0 58px;
}
li {
  text-align: justify-all;
}
.dados {
  margin: 0 50px;
  max-width: 500px;
  font-family: "Times New Roman", Times, serif;
}

.h3 {
  margin-top: 10px;
  margin-left: 110px;
  margin-bottom: 20px;
  font-family: "Times New Roman", Times, serif;
  font-size: 20px;
  font-weight: bold;
}

.imgufba {
  width: 40px;
  height: 60px;
}

.titulo {
  font: 400 16px bold;
  font-family: Arial, Helvetica, sans-serif;
}

.responsabilidade {
  font: 400 12px;
  font-family: Arial, Helvetica, sans-serif;

  margin-left: 50px;
  max-width: 500px;
}
.unidade {
  padding-left: 18px;
}
.assinatura {
  font: 400 12px;
  font-family: Arial, Helvetica, sans-serif;

  margin-left: 50px;
  max-width: 500px;
}
</style>