# Vue 学习仿写


#### [* 响应式原理仿写](https://github.com/wang90/vue_demo/blob/master/ref.html)
``````

class Dep {
    constructor() {
        this.deps = new Set();
    }
    depend() {
        if (active) {
            this.deps.add(active);
            console.log("注入")
        }
    }
    notify() {
        this.deps.forEach(dep => {dep()});
    }
}

function reacitve(obj){
    Object.keys(obj).forEach((key) => {
        if (obj.hasOwnProperty(key)) {
            let dep = new Dep();
            let value = obj[key]
            Object.defineProperty(vueData, key, {
                get() {
                    dep.depend();
                    return value;
                },
                set(newValue) {
                    value = newValue;
                    dep.notify();
                }
            });
        }
    });
    return vueData
}

function watch(cb){
    if ( typeof cb === "function") {
        active = cb;
        active();
        active = null;
    }
}
``````

