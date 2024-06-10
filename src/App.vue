<template>
  Hi. Take a look in the developer console.
</template>

<script>
import Streamify from 'streamify-string'
import { DataFactory, Store, StreamParser } from 'n3'
const { namedNode } = DataFactory

export default {
  name: 'AppView',
  data () {
    return {
      dataModel: {},
    }
  },
  mounted () {
    this.tryStore()
  },
  methods: {
    tryStore () {
      const streamParser = new StreamParser()
      let dataString = "<http://example.org/some> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/1999/02/22-rdf-syntax-ns#Class> ."
      Streamify(dataString).pipe(streamParser)

      const n3_store = new Store()
      n3_store.import(streamParser).on('end', () => {
        this.dataModel = n3_store
      })
    }
  }
}

</script>
