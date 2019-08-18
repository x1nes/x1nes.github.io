---
abbrlink: '0'
---


class EventBus {
    constructor(){
        this._event = new Map()
    }

    emit(type,...args){
        // console.log(this._event)
        const handlers = this._event.get(type)
        if(handlers) {
            handlers.forEach((fun)=>{
                if(args.length) {
                    fun.apply(this,args)
                }else{
                    fun.call(this)
                }
            })
        }
        return true
    }

    // 不能去掉匿名函数
    removeEventListener(type,listener){
        const handlers = this._event.get(type)
        if(handlers){
            this._event.set(type,handlers.filter(fun=>fun!==listener))
        }
    }

    addListener(type,listener){
        const handlers = this._event.get(type)
        if(handlers) {
            handlers.push(listener)
        } else {
            this._event.set(type,[listener])
        }
    }

    addListenerOnce(type,listener){
        const handlers = this._event.get(type)
        let run = false
        if(handlers) {
            handlers.push((...args)=>{
                !run && listener(...args)
                run = true
            })
        } else {
            this._event.set(type,[(...args)=>{
                !run && listener(...args)
                run = true
            }])
        }
    }
}

// test 

const emitter = new EventBus();

const hello = (name) =>{
    console.log(`hello ${name}`)
}

const helloOnce = (name) =>{
    console.log(`hello ${name}`)
}
const helloOnce2 = (name) =>{
    console.log(`hello ${name}`)
}

// 添加多个事件
emitter.addListener('arson', man => {
  console.log(`expel ${man}`);
});

emitter.addListener('arson', man => {
    console.log(`save ${man}`);
  });

emitter.emit('arson', 'low-end'); //


// 可以去掉事件

emitter.addListener('hello',hello);
emitter.emit('hello', 'world'); //
emitter.removeEventListener('hello',hello);
emitter.emit('hello', 'world2'); // 不打印

// 只执行一次
emitter.addListenerOnce('helloonce',helloOnce);
emitter.addListenerOnce('helloonce',helloOnce2);
emitter.emit('helloonce',"once");
emitter.emit('helloonce',"once");
emitter.emit('helloonce',"once");
emitter.emit('helloonce',"once");
emitter.emit('helloonce',"once2");
emitter.emit('helloonce',"once2");
emitter.emit('helloonce',"once2");

emitter.addListenerOnce('helloonce2',helloOnce2);
emitter.emit('helloonce2',"1");
emitter.emit('helloonce2',"2");
emitter.emit('helloonce2',"3");
emitter.emit('helloonce2',"4");