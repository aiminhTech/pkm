tags:: [[Effect TS]]

- https://effect.website/docs/runtime/
-
- ## Example RuntimeService in Angular
	- ```ts
	  import { Injectable, OnDestroy } from "@angular/core";
	  import { FetchHttpClient } from "@effect/platform";
	  import { Effect, Layer, ManagedRuntime, Option } from "effect";
	  import { RuntimeFiber } from "effect/Fiber";
	  
	  const RuntimeLayer = Layer.mergeAll(FetchHttpClient.layer);
	  export type RuntimeLayerSuccess = Layer.Layer.Success<typeof RuntimeLayer>;
	  
	  @Injectable({
	    providedIn: "root",
	  })
	  export class EffectRuntimeService implements OnDestroy {
	    rt: ManagedRuntime.ManagedRuntime<RuntimeLayerSuccess, never> | undefined = ManagedRuntime.make(RuntimeLayer)
	  
	    ngOnDestroy() {
	      this.rt?.dispose();
	      this.rt = undefined;
	    }
	    
	     public runSync<A, E>( effect: Effect.Effect<A, E, RuntimeLayerSuccess>): A {
	      if (this.rt) {
	        return this.rt.runSync(effect)
	      } else {
	        throw new Error("effect runtime is not initialized!")
	      }
	    }
	  
	    public runPromise<A, E>(
	      effect: Effect.Effect<A, E, RuntimeLayerSuccess>,
	    ): Promise<A> {
	      return this.rt
	        ? this.rt.runPromise(effect)
	        : Promise.reject("effect runtime is not initialized!");
	    }
	  
	    public runFork<A, E>(
	      effect: Effect.Effect<A, E, RuntimeLayerSuccess>,
	    ): Option.Option<RuntimeFiber<A, E>> {
	      return this.rt ? Option.some(this.rt.runFork(effect)) : Option.none();
	    }
	  }
	  ```