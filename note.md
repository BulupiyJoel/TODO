computed() : lui passer un getter et un setter

eg. export default {
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    }
  },
  computed: {
    fullName: {
      // accesseur
      get() {
        return this.firstName + ' ' + this.lastName
      },
      // mutateur
      set(newValue) {
        // Note : nous utilisons ici la syntaxe d'assignation par déstructuration.
        [this.firstName, this.lastName] = newValue.split(' ')
      }
    }
  }
}

note : on ne modifie pas les valeurs computed returner

**Ne pas utiliser v-for et v-if sur le meme element , v-if a une porter plus importante**

**On peut passer trois alias a v-for si on est dans un objet eg.(v,k,i) in Object*

+ Tout comme on peut utiliser v-for comme en pyhton en lui definissant une porter eg. v-for= n in 10
