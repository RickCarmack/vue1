<template>
    <div id='grid'>
      <h1>{{ heading }}</h1>
      <div class="table-responsive">
        <table class="table table-striped">
          <tr>
            <th v-for='items in columns'>&nbsp;&nbsp;{{items}}</th>
          </tr>
          <tbody>
            <tr v-for='items in people'>
              <td>{{items.name}}</td>
              <td>{{items.address}}</td>
              <td>{{items.phone}}</td>
              <td><a :href="`mailto:${items.email}`">{{items.email}}</a></td>
			  <td>{{items.entered}}</td>
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
      columns: ['Name', 'Address', 'Phone', 'Email', 'Entered'],
      people: [
        {name: 'Rick Carmack', address: '14436 Savoy Rd, Fayetteville AR, 72704', phone: '479.903.5502', email: 'riverguy64@gmail.com', entered: '1/20/2017'},
        {name: 'Susan Nemec', address: '1103 W Nursery Rd, Rogers AR, 72758', phone: '479.621.1586', email: 'susan.nemec@gmail.com', entered: '5/16/2017'},
        {name: 'Marc Wilson', address: '14438 Savoy Rd, Fayetteville, AR 72704', phone: '479.249.7294', email: 'marc.wilson@gmail.com', entered: '6/5/2017'},
        {name: 'Susie Wilson', address: '14438 Savoy Rd, Fayetteville, AR 72704', phone: '479.601.2411', email: 'martha.wilson@gmail.com', entered: '6/5/2017'},
		{name: 'Ella Wilson', address: '14438 Savoy Rd, Fayetteville, AR 72704', phone: '479.841.2341', email: 'ella.wilson@gmail.com', entered: '6/5/2017'}
        ]
    }},
  }
</script>
<style>
  th {
    text-align: left;
  }
  td {
    text-align: left;
  }
</style>
