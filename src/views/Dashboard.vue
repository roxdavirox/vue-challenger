<template>
  <div>
    <SubscriberWidgets />
    <CRow>
      <CCol :sm="12" :md="8">
        <CCard class="mb-4">
          <CCardBody>
            <CRow>
              <CCol :sm="5">
                <h4 id="traffic" class="card-title mb-0">Inscritos</h4>
                <div class="small text-medium-emphasis">Janeiro 2023</div>
              </CCol>
              <CCol :sm="7" class="d-none d-md-block">
                <CButton color="primary" class="float-end">
                  <CIcon icon="cil-cloud-download" />
                </CButton>
                <CButtonGroup
                  class="float-end me-3"
                  role="group"
                  aria-label="Basic outlined example"
                >
                  <CButton color="secondary" variant="outline">Day</CButton>
                  <CButton color="secondary" variant="outline" active
                    >Month</CButton
                  >
                  <CButton color="secondary" variant="outline">Year</CButton>
                </CButtonGroup>
              </CCol>
            </CRow>
            <CRow>
              <SubscribersChart
                style="height: 300px; max-height: 300px; margin-top: 40px"
              />
            </CRow>
          </CCardBody>
        </CCard>
      </CCol>
      <CCol :md="4" class="mb-4">
        <CCard>
          <CCardHeader>Cursos</CCardHeader>
          <CCardBody><CoursesChart /></CCardBody>
        </CCard>
      </CCol>
    </CRow>
  </div>
</template>

<script>
import SubscribersChart from './charts/SubscribersChart'
import SubscriberWidgets from './widgets/SubscriberWidgets'
import CoursesChart from '@/views/charts/CoursesChart'

export default {
  name: 'Dashboard',
  components: {
    SubscribersChart,
    SubscriberWidgets,
    CoursesChart,
  },
}
</script>
