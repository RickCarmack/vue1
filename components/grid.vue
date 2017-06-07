<template>
    <div id='grid'>
      <h1>{{ heading }}</h1>
      <div class="table-responsive">
        <table class="table table-striped">
          <tr>
            <th v-for='items in columns'>{{items}}</th>
          </tr>
          <tbody>
            <tr v-for='items in people'>
              <td>{{items.name}}</td>
              <td>{{items.address}}</td>
              <td>{{items.phone}}</td>
              <td>{{items.email}}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
</template>
<script>
  export default {
    name: 'grid',
    data (){
      return{
      heading: 'People List',
      columns: ['Name', 'Address', 'Phone', 'eMail'],
      people: [
        {name: 'Rick', address: '14436 Savoy Rd, Fayetteville AR, 72704', phone: '479.903.5502', email: 'riverguy64@gmail.com'},
        {name: 'Susan', address: '1103 W Nursery Rd, Rogers AR, 72758', phone: '479.621.1586', email: 'susan.nemec@gmail.com'},
        {name: 'Marc', address: '14438 Savoy Rd, Fayetteville, AR 72704', phone: 'none', email: 'marc.wilson@gmail.com'},
        {name: 'Susie', address: '14438 Savoy Rd, Fayetteville, AR 72704', phone: 'none', email: 'martha.wilson@gmail.com'}
        ]
    }},
  }
</script>
<style>
  th {
    text-align: center;
  }
  td {
    text-align: left;
  }
</style>
