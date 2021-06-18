<template>
  <div class="webpage__main">
    <Navigation />
    <Filterbar />
    <Form />
    <ExchangeCollapse />
  </div>
</template>

<script>
import Filterbar from '@/components/Filterbar'
import Form from '@/components/Form'
import ExchangeCollapse from '@/components/ExchangeCollapse'
import Navigation from '@/components/Navigation'

export default {
  components: {
    Navigation,
    Filterbar,
    Form,
    ExchangeCollapse,
  }
}
</script>
