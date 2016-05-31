##Grunt

###1 Grunt (global) Install
```
$ npm install -g grunt-cli
```

###2 Next, installing Grunt into local project
```
$ npm install grunt --save-dev
```

###3 Create grunt file
```
$ touch Gruntfile.js
```
**Here's the basic structure of a grunt file :**
```
module.exports = function(grunt) {

  // Configuration de Grunt
  grunt.initConfig({})

  // Définition des tâches Grunt
  grunt.registerTask('default', '')

}
```

###4 Add Grunt task : convert scss file to css

```
$ npm install grunt-contrib-sass --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {                              // Task's name
      dist: {                            // Sub-task's name
        options: {                       // Options
          style: 'expanded'
        },
        files: {                         // files's list
          'main.css': 'main.scss',       // 'target': 'source'
          'widgets.css': 'widgets.scss'
        }
      }
    }
  })

  // import
  grunt.loadNpmTasks('grunt-contrib-sass')

  // updating 'default' task which is running by defaul when grunt is running.
  // Here, we're define sass as a default task
  grunt.registerTask('default', ['sass:dist'])
}
```

**You can also give a folder instead of listing all the file one by one** 
```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{ // C'est ici que l'on définit le dossier que l'on souhaite importer
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')

  grunt.registerTask('default', ['sass:dist'])
}
```

###5 Add Grunt task : concataining all JS files

```
npm install grunt-contrib-concat --save-dev
```

**Adding package to grunt file**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-concat'); // New package

  grunt.registerTask('default', ['sass:dist'])
}
```

**Add new task**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';', // To insert ";" between each concatened file
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'], // Source
        dest: 'dist/built.js' // Target
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-concat');

  grunt.registerTask('default', ['sass:dist', 'concat:dist'])	// Add the new task in default task
}
```

###6 Add Grunt task : Compressing all JS files

```
$ npm install grunt-contrib-uglify --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')

  grunt.registerTask('dev', ['sass:dist', 'concat:dist']) // C'est pas chouette ça ?
  grunt.registerTask('dist', ['sass:dist', 'uglify:dist']) // Et hop, je compresse si je lance $ grunt dist
}
```

###7 Add automatic watcher

To avoid compilation after each file modification in your project, you can use a "watch" task.
```
$ npm install grunt-contrib-watch --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js']
        dest: 'dist/built.js'
      }
    },
    watch: {
      scripts: {
        files: '**/*.js', // All JS files
        tasks: ['concat:dist']
      },
      styles: {
        files: '**/*.scss', // All Sass files
        tasks: ['sass:dist']
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')
  grunt.loadNpmTasks('grunt-contrib-watch')

  grunt.registerTask('default', ['dev', 'watch'])
  grunt.registerTask('dev', ['sass:dist', 'concat:dist'])
  grunt.registerTask('dist', ['sass:dist', 'uglify:dist'])
}
```

###8 Cleaning Grunt file

```
module.exports = function(grunt) {

  // Je préfère définir mes imports tout en haut
  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')
  grunt.loadNpmTasks('grunt-contrib-watch')

  var jsSrc = ['src/intro.js', 'src/project.js', 'src/outro.js']
  var jsDist = 'dist/built.js'

  // Configuration de Grunt
  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      },
      dev: {} // À vous de le faire ! vous verrez que certaines options Sass sont plus intéressantes en mode dev que d'autres.
    },
    concat: {
      options: {
        separator: ';'
      },
      compile: { // On renomme vu qu'on n'a pas de mode dev/dist. Dist étant une autre tâche : uglify
        src: jsSrc, // Vu qu'on doit l'utiliser deux fois, autant en faire une variable.
        dest: jsDist // Il existe des hacks plus intéressants mais ce n'est pas le sujet du post.
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      compile: {
        src: jsSrc,
        dest: jsDist
      }
    },
    watch: {
      scripts: {
        files: '**/*.js',
        tasks: ['scripts:dev']
      },
      styles: {
        files: '**/*.scss',
        tasks: ['styles:dev']
      }
    }
  })

  grunt.registerTask('default', ['dev', 'watch'])
  grunt.registerTask('dev', ['styles:dev', 'scripts:dev'])
  grunt.registerTask('dist', ['styles:dist', 'scripts:dist'])

  // Give generics names
  grunt.registerTask('scripts:dev', ['concat:compile'])
  grunt.registerTask('scripts:dist', ['uglify:compile'])

  grunt.registerTask('styles:dev', ['sass:dev'])
  grunt.registerTask('styles:dist', ['sass:dist'])
}
```
