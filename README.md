# SASS :

- Stand for Syntactically Awesome Style Sheet
- it's preprocessor (compiled then go to the browser as css)

### Why SASS ?

- save time and make less errors
- more clear and organized code 
- using programming features (variables , functions, loops ...etc)



### Extentions 

- we need Live sass compiler on vs-code to compile sass to css
  


### Import And Use And Advanced Architecture

- we seperate our desing in folder called sass
- each page or component has sass file 
- the we import these pages inside main sass file using (import or use) word
- then we compile the main sass file to create main css file
  
  <pre>
      sass(folder)
      |_ pages (folder)
         |_ _contact.sass     (the name is _contact.sass we add the _ to ignore the compiling)
         |_ _home.sass
      main.sass
      main.css   (compiled file)
      main.map.css (compiled file)

      inside the main.sass file we will import pages files and it will converted to css

      main.sass
      @import './sass/pages/contact.sass'
      @use './sass/pages/home.sass'
  </pre>



### Declare variables

- we can declare variables by using $ before the variable name 
  <pre>
    $main-color : red ;
    $main-padding: 20px ;
  </pre>

- there are global & local scoop variables and we deal with it as same as js
- if there is variable declared local and i used it and put !global it will be global after this line
  <pre>
    .footer {
      $color : red !global;
      padding :10px;
    }
  </pre>

- i can define variables inside seperated file but when i imported it i import it with adding the following 
  <pre>

  use './path of sass file' as *

  .footer {
    color : variablename
  }

  because use doesnt see variables without this
  or i can use the name space if i dont want to add it :

    use './path of sass file'

  .footer {
    color : variableFileName.variablename
  }
  </pre>



  ###  Nesting And Parent Element 

- in css we nest elements like :
      <pre>
        .parent {
          //any thing 1
        }
        .parent .title {
          //any thing 2
        }
        .parent  .title p {
          //any thing 3
        }
      </pre>

- in sass we nest elements like :
      <pre>
        .parent {
          //any thing 1
          .title {
            //any thing 2
            p {
              //any thing 3
            }
          }
        }
      </pre>

- More examples 
  <pre>
  .parent-one,
  .parent-two {
    padding: 20px;
    .child {
      padding: 10px;
    }
  }

  .parent > {
    .child {
      font-size: 20px;
    }
    .test {
      font-weight: bold;
    }
  }

  .parent {
    > .child {
      font-size: 20px;
    }
    .test {
      font-weight: bold;
    }
    + p {
      font-size: 15px;
    }
  }

  .parent { > {
      .element-one {
        font-size: 10px;
      }
      .element-two {
        font-size: 10px;
      }
    }
    .not-direct-child {
      font-weight: bold;
    }
  }

  .box {
    .title {
      font-size: 10px;
    }
    .description {
      font-size: 8px;
    }
    &:hover {
      background-color: #eee;
    }
    &:hover .title {
      font-weight: bold;
    }

    &:hover {
      .title {
      font-weight: bold;
      }
    }

    :not(&) {
      font-weight: normal;
    }
    
    [dir="rtl"] & {
      direction: rtl;
    }
  }

  NOTE : & is related to the parent ( .box )
  </pre>


  ### Property Declarations And Placeholder

  - we can use this for properties if it has many values
  <pre>
    CSS:
      div {
        font-size : 20px;
        font-weight :bold;
        font-family : sans-arial
      }
      
    SASS:
      div {
        font {
          size: 20px;
          weight:bold;
          family: sans-arial;
        }
      }
  </pre>

- there is somthing used called place holder to store data that we need 
- place holder must start wih %
- we use @extend to get placeholder data any where we need

  <pre>
    %box-details {
      color : black;
      background-color: red;
      border-radius : 20px
    }

    .new-box {
      @extend %box-details;
      width :20px;
      height:20px
    }
    
    .title {
      @extend %box-details;
      font-weight : bold;
    }
  </pre>

### Control Flow => If And Else

  <pre>
    $theme: "dark";
    .page {
      @if $theme == "light" {
        background-color: white;
        color: #444;
      } @else if $theme == "dark"  {
        background-color: #444;
        color: white;
      } @else {
        @error('error here must dark or light')
      }
    }

    $rounded: false;
    .box {
      border-radius: if($rounded, 6px, 0px);
    }

    Note : if(condition, valueifTrue, valueifFalse)
  </pre>

### Interpolation
- To do interpolation we use it like this : #{any}
  <pre>
    $company: "falcon";
    $position: "right"; 
    
    .ad-#{$company} {
      font-size: 20px;
      background-image: url("imgs/#{$company}.png");
      #{$position}: 0;
    }
    
    IN CSS it looks like :

      .ad-falcon {
        font-size: 20px;
        background-image: url("imgs/falcon.png");
        right: 0;
      }
  </pre>

  ### comments 

  <pre>
    // This Comment Will Not Show In CSS File
    /* This Comment Will Show In CSS File But Not In Compressed Mode */
    /*! This Comment Will Show In CSS File And In Compressed Mode */
    /* This Comment Contains Interpolation => #{$company} افترض انه المتفير موجود */
     
    .box /* Multiple
    Lines
    Comment */ {
      font-size: 20px; // Inline Comment
    }
     
  </pre>