How to use
----------

Macro: `scope`
==============
    
    Syntax:
    
      scope(condition, {
          // code block
      });

      condition -> enum of type ScopeGuardType
                   exit: code block execute on exit from scope
                   success: code block execute on normal exit from scope
                   failure: code block execute on exception-induced exit from scope
    
    Example:
        
      scope(exit, {
          delete dynamicAllocatedInteger;
          delete dynamicAllocatedObject;
      });
    
      scope(success, {
          if (debug) saveToLog();
      });
    
      scope(failure, {
          rollback();
          delete cache;
      });
    
    
Macro: `release_container`
==========================
    
    Syntax:
    
      release_container(container_name);

    
Macro: `release_container_with_deleter`
=======================================
    
    Syntax:
    
      release_container_with_deleter(container_name, iterator_name {
      // custom clean up code
      });
    
      container_name: name of your container variable
      iterator_name: name of the iterator that you will address in the code block
    
    Example:
    
      map<int*, pair<int*, object*>> map_container;
      // ... allocate stuff
      release_container_with_deleter(map_container, itr, {
          delete itr->first;
          delete itr->second.first;
          delete itr->second.second;
      });