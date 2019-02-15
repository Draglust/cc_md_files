
# Reglas de validación

>Para usar estas reglas de validación se usará la siguiente llamada:
>$this->load->library(['validation/validationValidations' , 'form_validation' ]);
	$rules = ValidationValidations::getRules(\_\_FUNCTION\_\_);
>Tener en cuenta que el nombre de la función donde realicemos estas llamadas debe ser igual al índice del array $rules, y que los campos que vengan en el **POST** deben coincidir con los campos de dicho sub-array.


> La llamada a la función anterior (getRules(\_\_FUNCTION\_\_)) está declarada al final del fichero de validación.

    class  ValidationValidations  {
	    private  static  $rules  = array(
					    'validatePhone'  =>  [
						    ['field'  =>  'loan_number',
							 'label'  =>  'loan_number',
							 'rules'  =>  'required|is_numeric'],
						    ['field'  =>  'phone_number',
						     'label'  =>  'phone_number',
						     'rules'  =>  'required|is_numeric'],
					    ],
					    'getAddressConfirmation'  =>  [
						    ['field'  =>  'loan_number',
						     'label'  =>  'loan_number',
						     'rules'  =>  'required|is_numeric'],
						    ['field'  =>  'applicant_id',
						     'label'  =>  'applicant_id',
						     'rules'  =>  'required|is_numeric'],
						    ['field'  =>  'address',
						    'label'  =>  'address',
						    'rules'  =>  'required'],
					    ],
  
					    'validateEmail'  =>  [
						    ['field'  =>  'loan_number',
						    'label'  =>  'loan_number',
						    'rules'  =>  'required|is_numeric'],
						    ['field'  =>  'applicant_id',
						    'label'  =>  'applicant_id',
						    'rules'  =>  'required|is_numeric'],
						    ['field'  =>  'email',
						    'label'  =>  'email',
						    'rules'  =>  'required'],
					    ]
	    );
	    static  public  function  getRules($validation)  {
		    return  self::$rules[$validation];
	    }
    }

> Written with [StackEdit](https://stackedit.io/).
