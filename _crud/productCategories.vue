<template></template>

<script>
  export default {
    data() {
      return {
        crudId: this.$uid()
      }
    },
    computed: {
      crudData() {
        return {
          crudId: this.crudId,
          entityName: config("main.qcommerce.entityNames.productCategory"),
          apiRoute: 'apiRoutes.qcommerce.categories',
          permission: 'icommerce.categories',
          extraFormFields: 'Icommerce.crud-fields.productCategories',
          create: {
            title: this.$tr('qcommerce.layout.newCategory'),
          },
          read: {
            columns: [
              {name: 'id', label: this.$tr('ui.form.id'), field: 'id', style: 'width: 50px'},
              {name: 'name', label: this.$tr('ui.form.name'), field: 'title', align: 'rigth'},
              {name: 'slug', label: this.$tr('ui.form.slug'), field: 'slug', align: 'left'},
              {
                name: 'status', label: this.$tr('ui.form.status'), field: 'status'
              },
              {
                name: 'parent', label: this.$tr('ui.form.parent'), field: 'parent', align: 'left',
                format: val => val ? (val.title ? val.title : '-') : '-'
              },
              {
                name: 'created_at', label: this.$tr('ui.form.createdAt'), field: 'createdAt', align: 'left',
                format: val => val ? this.$trd(val) : '-',
              },
              {name: 'actions', label: this.$tr('ui.form.actions'), align: 'left'},
            ],
            requestParams: {
              include: 'parent',
              filter: {
                order: {
                  field: 'created_at',
                  way: 'desc',
                },
              },
            },
            filters : {
              parentId: {
                value: null,
                type: 'treeSelect',
                loadOptions: {
                  apiRoute: 'apiRoutes.qcommerce.categories',
                  select: {label: 'title', id: 'id'},
                },
                props: {
                  label: this.$tr('ui.form.parent'),
                  clearable: true
                }
              },
            }
          },
          update: {
            title: this.$tr('qcommerce.layout.updateCategory'),
            requestParams: {include: 'parent'}
          },
          delete: true,
          formLeft: {
            id: {value: ''},
            userId: {value: this.$store.state.quserAuth.userId},
            title: {
              value: '',
              type: 'input',
              isTranslatable: true,
              props: {
                label: `${this.$tr('ui.form.title')}*`,
                rules: [
                  val => !!val || this.$tr('ui.message.fieldRequired')
                ],
              }
            },
            slug: {
              value: '',
              type: 'input',
              isTranslatable: true,
              props: {
                label: `${this.$tr('ui.form.slug')}*`,
                rules: [
                  val => !!val || this.$tr('ui.message.fieldRequired')
                ],
              }
            },
            description: {
              value: '',
              type: 'html',
              isTranslatable: true,
              props: {
                label: `${this.$tr('ui.form.description')}*`,
                rules: [
                  val => !!val || this.$tr('ui.message.fieldRequired')
                ],
              }
            },
            metaTitle: {
              value: '',
              type: 'input',
              isTranslatable: true,
              props: {
                label: this.$tr('ui.form.metaTitle'),
              }
            },
            metaDescription: {
              value: '',
              type: 'input',
              isTranslatable: true,
              props: {
                label: this.$tr('ui.form.metaDescription'),
              }
            },
          },
          formRight: {
            masterRecord: {
              value: '0',
              isFakeField: true,
              type: 'select',
              props: {
                label: this.$tr('ui.form.masterRecord'),
                options: [
                  {label: this.$tr('ui.label.yes'), value: '1'},
                  {label: this.$tr('ui.label.no'), value: '0'},
                ]
              }
            },
            status: {
              value: '1',
              type: 'select',
              isTranslatable: false,
              props: {
                label: `${this.$tr('ui.form.status')}*`,
                options: [
                  {label: this.$tr('ui.label.enabled'), value: '1'},
                  {label: this.$tr('ui.label.disabled'), value: '0'}
                ],
                rules: [
                  val => !!val || this.$tr('ui.message.fieldRequired')
                ],
              }
            },
            parentId: {
              value: '0',
              type: 'treeSelect',
              loadOptions: {
                apiRoute: 'apiRoutes.qcommerce.categories',
                select: {label: 'title', id: 'id'}
              },
              props: {
                label: this.$tr('ui.form.parent'),
                clearable: false,
                options: [
                  {label: this.$tr('ui.label.disabled'), id: '0'},
                ],
              }
            },
            showMenu: {
              value: false,
              type: 'checkbox',
              props: {
                label: this.$tr('qcommerce.layout.form.showInMenu'),
              }
            },
            featured: {
              value: '0',
              type: 'checkbox',
              props: {
                label: this.$tr('qcommerce.layout.form.featured'),
                trueValue: '1',
                falseValue: '0',
              }
            },
            sortOrder: {
              value: '0',
              type: 'input',
              props: {
                label: this.$tr('qcommerce.layout.form.sortOrder'),
                type: 'number'
              }
            },
            mediasSingle: {
              name: 'mediasSingle',
              testId: 'mediasSingle',
              value: {},
              type: 'media',
              props: {
                label: this.$tr('ui.form.firstImage'),
                zone: 'mainimage',
                entity: "Modules\\Icommerce\\Entities\\Category",
                enitityId: null
              }
            },
            mediasSingle2: {
              name: 'mediasSingle',
              testId: 'mediasSingle2',
              value: {},
              type: 'media',
              props: {
                label: this.$tr('ui.form.secondaryImage'),
                zone: 'secondaryimage',
                entity: "Modules\\Icommerce\\Entities\\Category",
                enitityId: null
              }
            },
            view: {
              value: 1,
              isFakeField: true,
              type: 'select',
              props: {
                label: 'Vista de categoria',
                options: [
                  {label: 'Masonry', value: 0},
                  {label: 'Cuatro Columnas', value: 1},
                  {label: 'Tres Columnas', value: 2},
                  {label: 'Dos Columnas', value: 3},
                ]
              }
            },
          },
        }
      },
      //Crud info
      crudInfo() {
        return this.$store.state.qcrudComponent.component[this.crudId] || {}
      }
    }
  }
</script>
