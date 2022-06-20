# Digital-Notes-Application-Hilt

*flow :
whenever the applications gets start the hilt will gets initialize.

@HiltAndroidApp
class NoteApplication: Application() {
}


*NavHost basically a container in which different fragments will be shown based on logic.

*NavGraph will determine how the fragments will get move.

*buildFeatures {viewBinding = true}

If view binding is enabled for a module, 
a binding class is generated for each XML layout file that the module contains.
Each binding class contains references to the root view and all views that have an ID. 
The name of the binding class is generated by converting the name of the XML file to Pascal case and adding the word "Binding" to the end.

*For example, given a layout file called result_profile.xml:

The generated binding class is called ResultProfileBinding.

(<LinearLayout
        ...
               
    ...
               
</LinearLayout>)



*Every binding class also includes a getRoot() method,

 providing a direct reference for the root view of the corresponding layout file. 
 
 In this example, the getRoot() method in the ResultProfileBinding class returns the LinearLayout root view.

private lateinit var binding: ResultProfileBinding

override fun onCreate(savedInstanceState: Bundle?) {

    super.onCreate(savedInstanceState)
    binding = ResultProfileBinding.inflate(layoutInflater)
    val view = binding.root
    setContentView(view)
    
}


*static inflate() method included in the generated binding class. 
 This creates an instance of the binding class for the activity to use.

*Get a reference to the root view by either calling the getRoot() method.

*Pass the root view to setContentView() to make it the active view on the screen.

*View binding has important advantages over using findViewById:

 |->Null safety: Since view binding creates direct references to views, 
    there's no risk of a null pointer exception due to an invalid view ID.

 |->Type safety: In findViewById<TextView>(R.id.sample_text)we have to mention type 
                 In future if we change the type then it will throw error,
                 Using View binding there's no risk of a class cast exception. 




===============
  
class RegisterFragment : Fragment() {

    private var _binding : FragmentRegisterBinding? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {

        _binding = FragmentRegisterBinding.inflate(inflater,container,false)

        _binding.textview //add non null asserted(!!) call 
        return inflater.inflate(R.layout.fragment_register, container, false)
    }

}


Solution 1:

 private var _binding : FragmentRegisterBinding? = null
  
 _binding!!.textview



Solution 2:

 private var _binding : FragmentRegisterBinding? = null
  
 private val binding get() = _binding !!

 binding.textview

========================

 *Create a binding object

 private var _binding : FragmentRegisterBinding? = null
  
 private val binding get() = _binding !!

 *Initialize binding object in onCreateView

 _binding = FragmentRegisterBinding.inflate(inflater,container,false)
