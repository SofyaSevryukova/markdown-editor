<template>
  <v-container style="padding: 0" fluid>
    <v-layout row wrap>

      <v-flex xs12 :md6="preview" class="pa-3">
        <v-layout column>
          <v-card class="min-height">
            <v-textarea
                solo
                flat
                hide-details
                auto-grow
                ref="textarea"
                :value="value"
                @input="val => $emit('input', val)"
            />
          </v-card>
        </v-layout>
      </v-flex>

      <v-flex xs12 :md6="preview" class="pa-3">
          <v-card class="min-height">
            <v-card-text v-if="mode === 'Rendered'" class="subheading markdown-text" v-html="compiled"/>
            <v-card-text v-else-if="mode === 'Source'" class="subheading">
              {{ compiled }}
            </v-card-text>
          </v-card>
      </v-flex>

    </v-layout>
  </v-container>
</template>

<style scoped>
  .v-textarea >>> .v-input__control > .v-input__slot {
    border-top-left-radius: 0;
    border-top-right-radius: 0;
  }
  .min-height {
    min-height: 300px;
  }

</style>

<script>
    import marked from '../util/marked.js';
    import {VContainer, VLayout, VFlex, VCard, VCardText, VTextarea} from 'vuetify/lib';
    // Стили

    import '../style.css';

    export default {
        components: {
            VContainer,
            VLayout,
            VFlex,
            VCard,
            VCardText,
            VTextarea
        },
        props: {
            value: {
                type: String,
                default: ''
            },
            mode: {
                type: String,
                default: 'Rendered'
            },
            outline: {
                type: Boolean,
                default: false
            },
            color: {
                type: String,
                default: undefined
            },
            preview: {
                type: Boolean,
                default: true
            }
        },
        computed: {
            compiled() {
                return marked(this.value);
            }
        },

        methods: {
            focus() {
                this.$refs.textarea.focus();
            }
        }
    };
</script>
