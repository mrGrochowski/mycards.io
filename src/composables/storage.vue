<script>
import { PouchDB } from '@svouch/pouchdb'

const db = new PouchDB('test_db1')
export const setBase = () => {

  db.info((err, info) => {
    if (!err) {
      console.log(info)
    }
  })
}

export const writeToBase = ()=> {

  const testowe = {
    _id: 'cos',
    title: "text",
    completed: false
  };

  db.put(testowe, function callback(err, result) {
    if (!err) {
      console.log('Successfully posted a todo!');
    }
  });

}


export const  getFromBase = async ()=>{

  const result = await db.get('cos')
  console.log(result);

}
</script>
