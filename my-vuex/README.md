# 仿写 vuex


````

class  Store {
    constructor( options= {} ) {
        let { state , mutations } = options;
        this._vm = reactive( state );
        this._mutations = mutations;
    }
    get state() {
        return this._vm;
    }
    commit ( type, payload ) {
        const entry = this._mutations[ type ];
        if ( !entry ) {
            return; 
        }
        entry( this.state, payload );
    }
}


````
