<template></template>
<script>
  export default {
    data(){
      return {
        types:  {
          0: this.$tr('ui.label.no'),
          1: this.$tr('ui.label.yes'),
        }
      }
    },
    computed: {
      crudData() {
        return {
          entityName: config("main.qcommerce.entityNames.coupon"),
          apiRoute: 'apiRoutes.qcommerce.coupons',
          permission: 'icommerce.coupons',
          extraFormFields: 'Icommerce.crud-fields.coupons',
          create: {
            title: this.$tr('qcommerce.layout.newCoupon'),
            to: {name: 'qcommerce.admin.coupons.create'}
          },
          read: {
            columns: [
              {name: 'id', label: this.$tr('ui.form.id'), field: 'id', align: 'left'},
              {name: 'code', label: this.$tr('qcommerce.layout.form.code'), field: 'code', align: 'left'},
              {name: 'quantityTotal', label: this.$tr('qcommerce.layout.form.quantityTotal'), field: 'quantityTotal', align: 'left'},
              {
                name: 'discount', label: this.$tr('qcommerce.layout.form.discount'), field: 'discount', align: 'left',
                format: (val,row) => val ? row.criteria == 'percentage' ? this.$n(val/100, 'percent') : this.$trc(val) : '-',
              },
              {name: 'dateStart', label: this.$tr('qcommerce.layout.form.dateStart'), field: 'dateStart', align: 'left'},
              {name: 'dateEnd', label: this.$tr('qcommerce.layout.form.dateEnd'), field: 'dateEnd', align: 'left'},
              {
                name: 'running', label: this.$tr('qcommerce.layout.form.running'), field: 'running', align: 'left',
                format: val => val ? this.$tr('qcommerce.layout.options.yes') : this.$tr('qcommerce.layout.options.no'),
              },
              {
                name: 'finished', label: this.$tr('qcommerce.layout.form.finished'), field: 'finished', align: 'left',
                format: val => val ? this.$tr('qcommerce.layout.options.yes') : this.$tr('qcommerce.layout.options.no'),
              },
              {name: 'quantityTotalCustomer', label: this.$tr('qcommerce.layout.form.quantityTotalCustomer'), field: 'quantityTotalCustomer', align: 'left'},
              {name: 'type', label: this.$tr('qcommerce.layout.form.allOrder'), field: 'type', align: 'left', format: val => this.types[val ?? 0]},
              {name: 'actions', label: this.$tr('ui.form.actions'), align: 'right'},
            ],
            requestParams: {},
            filters: {},
          },
          update: {
            to : 'qcommerce.admin.coupons.edit'
          },
          delete: true,
          formLeft: {},
        }
      },
    }
  }
</script>
