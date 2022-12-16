<template>
  <v-app>
    <v-main>
      <p id="important">
        Все шифры работают корректно ТОЛЬКО с английским алфавитом <br />
        ABCDEFGHIJKLMNOPQRSTUVWXYZ
      </p>
      <v-container>
        <v-layout row wrap>
          <v-col id="buttons" col="4">
            <v-btn
              id="Cipher1"
              color="#101357"
              class="white--text"
              @click="cipher1()"
              >Шифр Замены №1</v-btn
            >
            <br />
            <v-btn
              id="Cipher2"
              color="#101357"
              class="white--text"
              @click="cipher2()"
              >Шифр Замены №2</v-btn
            >
            <br />
            <v-btn
              id="Cipher3"
              color="#101357"
              class="white--text"
              @click="cipher3()"
              >Шифр Замены №3</v-btn
            >
            <br />
            <v-btn
              id="Cipher4"
              color="#101357"
              class="white--text"
              @click="cipher4()"
              >Шифр Замены №4</v-btn
            >
            <br />
            <v-btn
              id="Cipher5"
              color="#101357"
              class="white--text"
              @click="cipher5()"
              >Шифр Перестановки №1</v-btn
            >
            <br />
            <v-btn
              id="Cipher6"
              color="#101357"
              class="white--text"
              @click="cipher6()"
              >Шифр Перестановки №2</v-btn
            >
            <br />
            <v-btn
              id="Cipher7"
              color="#101357"
              class="white--text"
              @click="cipher7()"
              >Шифр Гаммирования</v-btn
            >
          </v-col>
          <v-col id="inputs" col="8">
            <v-text-field
              background-color="white"
              label="Открытый текст"
              v-model="inputCipher"
              outlined
              dense
              class="shrink"
              style="margin-top: 10px"
            >
            </v-text-field>
            <v-text-field
              background-color="white"
              label="Зашифрованный текст"
              v-model="inputDecipher"
              outlined
              dense
              class="shrink"
            >
            </v-text-field>
            <v-text-field
              background-color="white"
              v-if="cipher2Flag || cipher3Flag"
              label="a"
              v-model="paramA"
              outlined
              dense
              class="shrink"
            >
            </v-text-field>
            <v-text-field
              background-color="white"
              v-if="cipher3Flag"
              label="Ключевое слово"
              v-model="paramKeyword"
              outlined
              dense
              class="shrink"
            >
            </v-text-field>

            <v-text-field
              background-color="white"
              v-if="cipher2Flag"
              label="b"
              v-model="paramB"
              outlined
              dense
              class="shrink"
            >
            </v-text-field>

            <v-text-field
              background-color="white"
              v-if="cipher1Flag || cipher4Flag || cipher7Flag"
              label="Ключ"
              v-model="paramKey"
              outlined
              dense
              class="shrink"
            >
            </v-text-field>

            <v-btn
              id="cipher"
              color="#101357"
              class="white--text"
              @click="cipherText()"
              >Зашифровать</v-btn
            >
            <v-btn
              style="margin-left: 10px"
              id="dechiper"
              color="#101357"
              class="white--text"
              @click="decipherText()"
              >Расшифровать</v-btn
            >
            <v-text-field
              
              background-color="white"
              label="Зашифрованный/Расшифрованный текст"
              v-model="output"
              outlined
              dense
              class="shrink"
              style="margin-top: 30px"
              disabled
            >
            </v-text-field>
          </v-col>
        </v-layout>
      </v-container>
      <br />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    alphabet: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
    inputCipher: "",
    inputDecipher: "",
    output: "",
    cipher1Flag: false,
    cipher2Flag: false,
    cipher3Flag: false,
    cipher4Flag: false,
    cipher5Flag: false,
    cipher6Flag: false,
    cipher7Flag: false,
    paramA: "",
    paramB: "",
    paramKey: "",
    paramKeyword: "",
  }),

  methods: {
    setFlagsFalse() {
      this.cipher1Flag = false;
      this.cipher2Flag = false;
      this.cipher3Flag = false;
      this.cipher4Flag = false;
      this.cipher5Flag = false;
      this.cipher6Flag = false;
      this.cipher7Flag = false;
      this.output = "";
    },
    clearInputs() {
      this.inputCipher = "";
      this.inputDecipher = "";
      this.paramA = "";
      this.paramB = "";
      this.paramKey = "";
      this.paramKeyword = "";
    },
    cipher1() {
      this.setFlagsFalse();
      this.cipher1Flag = true;
    },
    cipher2() {
      this.setFlagsFalse();
      this.cipher2Flag = true;
    },
    cipher3() {
      this.setFlagsFalse();
      this.cipher3Flag = true;
    },
    cipher4() {
      this.setFlagsFalse();
      this.cipher4Flag = true;
    },
    cipher5() {
      this.setFlagsFalse();
      this.cipher5Flag = true;
    },
    cipher6() {
      this.setFlagsFalse();
      this.cipher6Flag = true;
    },
    cipher7() {
      this.setFlagsFalse();
      this.cipher7Flag = true;
    },
    cipherText() {
      if (this.cipher1Flag) {
        let str = this.inputCipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);
          if (this.alphabet.includes(curChar)) {
            result += this.alphabet.charAt(
              (alphIndex + parseInt(this.paramKey)) % this.alphabet.length
            );
          } else {
            result += curChar;
          }
        }
        this.output = result;
      } else if (this.cipher2Flag) {
        let str = this.inputCipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);
          if (this.alphabet.includes(curChar)) {
            result += this.alphabet.charAt(
              (alphIndex * parseInt(this.paramA) + parseInt(this.paramB)) %
                this.alphabet.length
            );
          } else {
            result += curChar;
          }
        }
        this.output = result;
      } else if (this.cipher3Flag) {
        let newAlph = "                          ".split('');
        let position = parseInt(this.paramA);
        let filledLetters = 0;
        let indexKeyWord = 0;
        let str = this.inputCipher.toUpperCase();
        let result = "";

        while(filledLetters < 26){
          if(indexKeyWord < this.paramKeyword.length){
            newAlph[position % 26] = this.paramKeyword.charAt(indexKeyWord++);
            position++;
          }
          if(indexKeyWord == this.paramKeyword.length){
            if(!newAlph.join('').includes(this.alphabet.charAt(filledLetters))){
              newAlph[position%26] = this.alphabet.charAt(filledLetters);
              position++
            }
            filledLetters++;
          }
        }

        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);
          if(this.alphabet.includes(curChar)){
            result += newAlph.join('').charAt(alphIndex)
          } else {
            result += curChar;
          }
        }
        this.output = result;

      } else if (this.cipher4Flag) {
        let str = this.inputCipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);

          if (this.alphabet.includes(curChar)){
            result += this.alphabet.charAt((alphIndex + 
                      this.alphabet.charCodeAt(this.paramKey.charCodeAt(i % this.paramKey.length) % 26)) 
                      % this.alphabet.length)
                                          
          } else{
            result += curChar;
          }
        }
        this.output = result;

      } else if (this.cipher5Flag) {
          let str = this.inputCipher;
          let sizeStr = str.length;
          let countDiv3 = Math.floor(sizeStr / 3);

          function encryptHelper(countDiv3, openText, b){
            let crypt = "";
            let crypt1 = "";
            let crypt2 = "";
            let crypt3 = "";

            for (let j = 0; j < countDiv3; j++) {
              crypt1 += openText.charAt(j)
              crypt2 += openText.charAt(j + countDiv3)
              crypt3 += openText.charAt(j + 2 * countDiv3)
            }

            let cryptArray1 = crypt1.split('');
            let cryptArray2 = crypt2.split('');
            let cryptArray3 = crypt3.split('');

            for (let i1 = 0, i2 = 0, i3 = 0; i1 < countDiv3 && i2 < countDiv3 && i3 < countDiv3; i1++, i2++, i3++){
              crypt += cryptArray3[i3];
              crypt += cryptArray2[i2];
              crypt += cryptArray1[i1];
            }

            if(b){
              let t1 = openText.length - (openText.length % 3); //3
              let t2 = openText.length //4
              crypt = crypt.slice(0, t1) + openText.slice(t1,t2) + crypt.slice(t2)
            }

            return crypt;

          }

          if(sizeStr % 3 === 0){
            str = encryptHelper(countDiv3, this.inputCipher, false);
          } else if (sizeStr > 3){
            str = encryptHelper(countDiv3, this.inputCipher, true )
          }

          this.output = str;

      } else if (this.cipher6Flag) {
        let str = this.inputCipher;
        let result = "";
        function encryptHelper(openText){
          let crypt1 = "";
          let crypt2 = "";
          let crypt3 = "";

          for (let i = 0;; i++) {
            if(i*4 >= openText.length){
              break;
            }
            crypt3 += openText.charAt(i*4)
          }

          for (let i = 0;; i++) {
            if((1+i*2) >= openText.length){
              break;
            }
            crypt2 += openText.charAt(1+i*2)
          }

          for (let i = 0;; i++) {
            if((2+i*4) >= openText.length){
              break;
            }
            crypt1 += openText.charAt(2+i*4)
          }

          return crypt1 + crypt2 + crypt3
        }
        
        result = encryptHelper(str);
        this.output = result;
      } else if (this.cipher7Flag) {
        let result = "";
        let str = this.inputCipher.toUpperCase();

        for (let i = 0; i < str.length; i++) {
          let curCharInt = this.alphabet.indexOf(str.charAt(i));
          let keyCharInt = this.alphabet.indexOf(this.paramKey.charAt(i%this.paramKey.length));

          if(this.alphabet.includes(str.charAt(i))){
            result += this.alphabet.charAt(curCharInt ^ keyCharInt);
          } else {
            result += str.charAt(i);
          }
        }
        this.output = result;
      }
    },
    decipherText() {
      if (this.cipher1Flag) {
        let str = this.inputDecipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);
          if (this.alphabet.includes(curChar)) {
            result += this.alphabet.charAt(
              (alphIndex + (26 - parseInt(this.paramKey))) %
                this.alphabet.length
            );
          } else {
            result += curChar;
          }
        }
        this.output = result;
      } else if (this.cipher2Flag) {
        let str = this.inputDecipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar);
          if (this.alphabet.includes(curChar)) {
          if (alphIndex >= parseInt(this.paramB)) {
            result += this.alphabet.charAt(
            ((alphIndex - parseInt(this.paramB)) * parseInt(this.paramA) * parseInt(this.paramA)) % this.alphabet.length);
          } else{
            result += this.alphabet.charAt(((alphIndex + this.alphabet.length - parseInt(this.paramB)) *
                  parseInt(this.paramA) * parseInt(this.paramA)) % this.alphabet.length)
          }
        } else {
          result += curChar;
        }
        }
        this.output = result;

      } else if (this.cipher3Flag) {
        let newAlph = "                          ".split(',');
        let position = parseInt(this.paramA);
        let filledLetters = 0;
        let indexKeyWord = 0;
        let str = this.inputDecipher.toUpperCase();
        let result = "";

        while(filledLetters < 26){
          if(indexKeyWord < this.paramKeyword.length){
            newAlph[position % 26] = this.paramKeyword.charAt(indexKeyWord++);
            position++;
          }
          if(indexKeyWord == this.paramKeyword.length){
            if(!newAlph.join('').includes(this.alphabet.charAt(filledLetters))){
              newAlph[position%26] = this.alphabet.charAt(filledLetters);
              position++
            }
            filledLetters++;
          }
        }

        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = newAlph.join('').indexOf(curChar);
          if(this.alphabet.includes(curChar)){
            result += this.alphabet.charAt(alphIndex);
          } else {
            result += curChar;
          }
        }
        this.output = result;
      } else if (this.cipher4Flag) {
        let str = this.inputDecipher.toUpperCase();
        let result = "";
        for (let i = 0; i < str.length; i++) {
          let curChar = str.charAt(i);
          let alphIndex = this.alphabet.indexOf(curChar)
          if(this.alphabet.includes(curChar)){
            let keyIndex = this.paramKey.charCodeAt(i % this.paramKey.length) % 26;
            let some = alphIndex +  (26*1000)  - this.alphabet.charCodeAt(keyIndex);
            result += this.alphabet.charAt(some % 26)
          } else {
            result += curChar;
          }
          this.output = result;
        }
      } else if (this.cipher5Flag) {
        let str = this.inputDecipher;
        let sizeStr = str.length;
        let countDiv3 = Math.floor(sizeStr / 3);

        function decryptHelper(countDiv3, crypt, b){
          let openText = "";
          let end = "";

          let crypt1 = "";
          let crypt2 = "";
          let crypt3 = "";

          let t1 = crypt.length - (crypt.length % 3);
          let t2 = crypt.length;
          end = crypt.slice(t1,t2)
          openText = crypt.slice(0,t1);

          for (let i = 0; i < countDiv3; i++) {
            crypt1 += openText.charAt(3 * i + 2); 
          }
          for (let i = 0; i < countDiv3; i++) {
            crypt2 += openText.charAt((3 * i) + 1); 
          }
          for (let i = 0; i < countDiv3; i++) {
            crypt3 += openText.charAt(3 * i); 
          }

          return crypt1+crypt2+crypt3+end;
        }

        if(sizeStr % 3 === 0){
          str = decryptHelper(countDiv3, str, false)
        } else if (sizeStr > 3){
          str = decryptHelper(countDiv3, str, true)
        } 

        this.output = str;

      } else if (this.cipher6Flag) {
        let str = this.inputDecipher;
        let result = "";

        function decryptHelper(crypt){
          let openText = "";

          let crypt1 = "";
          let crypt2 = "";
          let crypt3 = "";

          let range1 = Math.floor((((crypt.length) - 2) / 5)) + 1;
          let range2 = Math.floor(crypt.length / 2);

          for (let i = 0; i < range1; i++) {
            crypt3 += crypt.charAt(i)
          }

          for (let i = range1; i < range1 + range2; i++) {
            crypt2 += crypt.charAt(i)
          }

          for (let i = range1 + range2; i < crypt.length; i++) {
            crypt1 += crypt.charAt(i)
          }

          let prevIdent = 1;
          let ident = 1;
          let i1 = 0;
          let i2 = 0;
          let i3 = 0;

          for (let i = 0; i < crypt.length; i++) {
            switch(ident){
              case 1:
                openText+=crypt1.charAt(i1);
                i1++;
                prevIdent=1;
                ident=2;
                break;
              case 2:
                openText+=crypt2.charAt(i2);
                if(prevIdent === 1){
                  ident = 3;
                } else {
                  ident = 1;
                }
                i2++;
                break;
              case 3:
                openText+=crypt3.charAt(i3);
                i3++;
                prevIdent = 3;
                ident = 2;
                break;
            }
            
          }

          return openText;

        }

        result = decryptHelper(str);
        this.output = result


      } else if (this.cipher7Flag) {
        let result = "";
        let str = this.inputDecipher.toUpperCase();

        for (let i = 0; i < str.length; i++) {
          let curCharInt = this.alphabet.indexOf(str.charAt(i));
          let keyCharInt = this.alphabet.indexOf(this.paramKey.charAt(i%this.paramKey.length));

          if(this.alphabet.includes(str.charAt(i))){
            result += this.alphabet.charAt(curCharInt ^ keyCharInt);
          } else {
            result += str.charAt(i);
          }
        }
        this.output = result;
      }
    },
  },
};
</script>

<style>
#important {
  color: white;
  border-radius: 10px;
  border-width: 50;
  text-align: center;
  background-color: #f83636;
  background-size: 20%;
  width: 60;
  margin-left: 10px;
  margin-right: 10px;
  margin-top: 10px;
}
.v-btn {
  margin-top: 10px;
}
.v-main {
  background-color: #cc8c58;
  font-family: "Avenir", Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothig: grayscale;
  color: #2c3e50;
}
</style>
