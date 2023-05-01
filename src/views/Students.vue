import { computed } from 'vue';
<template>
  <CRow>
    <CCol :xs="12">
      <CModal
        :visible="modalVisible"
        @close="
          () => {
            modalVisible = false
          }
        "
      >
        <CModalHeader
          dismiss
          @close="
            () => {
              modalVisible = false
            }
          "
        >
          <CModalTitle>Ingressante</CModalTitle>
        </CModalHeader>
        <CModalBody>
          <CCol :xs="12">
            <CCard class="mb-4">
              <CCardHeader>
                <strong>Cadastrar novo ingressante</strong>
              </CCardHeader>
              <CCardBody>
                <CForm>
                  <div class="mb-3">
                    <CFormLabel for="nameInput">Nome</CFormLabel>
                    <CFormInput
                      id="nameInput"
                      type="text"
                      placeholder="Nome do ingressante"
                      v-model="name"
                      @change="changeName"
                    />
                  </div>
                  <div class="mb-3">
                    <CFormLabel for="courseSelect">Curso</CFormLabel>
                    <CFormSelect id="courseSelect" v-model="courseSelected">
                      <option
                        v-for="(course, index) in courses"
                        :key="index"
                        :value="index"
                      >
                        {{ course }}
                      </option>
                    </CFormSelect>
                  </div>
                  <div class="mb-3">
                    <CFormLabel for="stateSelect">Estados</CFormLabel>
                    <CFormSelect id="stateSelect" v-model="stateSelected">
                      <option
                        v-for="(state, index) in states"
                        :key="index"
                        :value="index"
                      >
                        {{ state }}
                      </option>
                    </CFormSelect>
                  </div>
                  <div class="mb-3">
                    <CFormLabel for="citySelect">Cidade</CFormLabel>
                    <CFormSelect id="citySelect" v-model="citySelected">
                      <option
                        v-for="(city, index) in cities[
                          Object.keys(cities)[stateSelected]
                        ]"
                        :key="index"
                        :value="index"
                      >
                        {{ city }}
                      </option>
                    </CFormSelect>
                  </div>
                </CForm>
              </CCardBody>
            </CCard>
          </CCol>
        </CModalBody>
        <CModalFooter>
          <CButton
            color="secondary"
            @click="
              () => {
                modalVisible = false
              }
            "
          >
            Voltar
          </CButton>
          <CButton @click="saveStudent" color="primary">Gravar</CButton>
        </CModalFooter>
      </CModal>
    </CCol>
    <CCol :xs="12">
      <CCard class="mb-4">
        <CCardHeader>
          <div class="d-flex justify-content-between">
            <div><strong>Lista de ingressantes</strong></div>
            <div>
              <CButton
                color="primary"
                @click="
                  () => {
                    modalVisible = true
                  }
                "
              >
                Cadastrar ingressante
              </CButton>
            </div>
          </div>
        </CCardHeader>
        <CCardBody>
          <CTable>
            <CTableHead>
              <CTableRow>
                <CTableHeaderCell scope="col">#</CTableHeaderCell>
                <CTableHeaderCell scope="col">Nome</CTableHeaderCell>
                <CTableHeaderCell scope="col">Curso</CTableHeaderCell>
                <CTableHeaderCell scope="col">Estado</CTableHeaderCell>
                <CTableHeaderCell scope="col">Cidade</CTableHeaderCell>
              </CTableRow>
            </CTableHead>
            <CTableBody>
              <CTableRow v-for="(student, index) in students" :key="student.id">
                <CTableHeaderCell scope="row">{{ index + 1 }}</CTableHeaderCell>
                <CTableDataCell>{{ student.name }}</CTableDataCell>
                <CTableDataCell>{{ student.course }}</CTableDataCell>
                <CTableDataCell>{{ student.state }}</CTableDataCell>
                <CTableDataCell>{{ student.city }}</CTableDataCell>
              </CTableRow>
            </CTableBody>
          </CTable>
        </CCardBody>
      </CCard>
    </CCol>
  </CRow>
</template>

<script>
export default {
  name: 'Tables',
  data() {
    return {
      modalVisible: false,
      name: '',
      courses: ['Matemática', 'Letras', 'Geografia'],
      states: ['São Paulo', 'Rio de Janeiro', 'Minas Gerais'],
      cities: {
        sp: ['Mogi das Cruzes', 'Suzano', 'Poá', 'Guararema'],
        rj: ['Angra dos Reis', 'Niterói', 'Itaboraí'],
        mg: ['Belo Horizonte', 'Monte Azul', 'Muzambinho'],
      },
      stateSelected: 0,
      courseSelected: 0,
      citySelected: 0,
      students: [
        {
          id: 1,
          name: 'Mark',
          course: 'Matemática',
          state: 'São Paulo',
          city: 'Mogi das Cruzes',
        },
        {
          id: 2,
          name: 'Jacob',
          course: 'Letras',
          state: 'São Paulo',
          city: 'Suzano',
        },
        {
          id: 3,
          name: 'Larry the Bird',
          course: 'Geografia',
          state: 'São Paulo',
          city: 'Poá',
        },
      ],
    }
  },

  methods: {
    clearStudentState() {
      this.name = ''
      this.courseSelected = 0
      this.stateSelected = 0
      this.citySelected = 0
    },

    saveStudent() {
      const newStudent = {
        id: this.students[this.students.length - 1].id + 1 || 0,
        name: this.name,
        course: this.courses[this.courseSelected],
        state: this.states[this.stateSelected],
        city: Object.values(this.cities)[this.stateSelected][this.citySelected],
      }
      this.students.push(newStudent)
      this.modalVisible = false
      console.log(newStudent)
      this.clearStudentState()
    },

    changeName(event) {
      this.name = event.target.value
    },
  },
}
</script>
