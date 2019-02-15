# Función receptora
> Se reciben los parámetros por Post, se pasan a la función que ejecuta (que tiene el mismo nombre a excepción de "**_post**") y se guardan las dos variables de respuesta (**$response , $code**).
> Luego se devuelve un JSON con dichas variables.

	public  function  validatePhone_post() {
		list($response , $code) = $this->validatePhone( post() );
		outputJson( $response , $code );
	}
	
# Función principal

> Esta función es la que hace todo el pre-proceso de validación.
> Realiza una llamada a una librería con reglas de validación,  y si la validación es correcta realiza los siguientes pasos se realizan, en caso contrario se devuelven los mensajes de error formados.

	public  function  validatePhone($data){
		$code = self::HTTP_VALIDATION_ERROR;
		$this->load->library(['validation/validationValidations' , 'form_validation' ]);
		$rules = ValidationValidations::getRules(__FUNCTION__);
		$response = ['status' => _KO];
		if ( $this->form_validation->validateData($data,$rules)) {
			list( $loan , $app ) = $this->getLoanInfo($data['loan_number']);
			$this->config->load('validation/'.ENVIRONMENT.'/config' );
			$credentials = $this->config->item('phone_api_config');
			$resp = $this->validation_service->validatePhone($data , $credentials);
			$code  =  self::HTTP_OK;
		}else {
			$response['message'] = $this->form_validation->error_array();
			$code = self::HTTP_VALIDATION_ERROR;
		}
		return [$response , $code];
	}

> *Explicación de ValidationValidations::getRules(\_\_FUNCTION\_\_)
> Llamada a la función **getRules** en la clase ValidationValidations (*véase mayúsculas*), con el parámetro \_\_FUNCION\_\_ que hace referencia al nombre de la función donde está contenida esta llamada.

	$config['phone_api_config']  =  [
		'user'  =>  'checkphone@dineo.es',
		'pass'  =>  'XXXXXXXXXXXXX'
	];
	//ESTA LINEA ESTÁ EN EL CÓDIGO DE LA FUNCIÓN, NO PERTENECE A LA CARGA DE VARIABLES DE CONFIGURACION
	$credentials = $this->config->item('phone_api_config');
> *Explicación de $credentials =  $this->config->load('validation/'.ENVIRONMENT.'/config' )
> Carga de las variables de configuración en base al entorno en el que nos encontremos.
> 
> Las variables las cogeremos  utilizando el nombre que le hayamos puesto como índice, que será igualmente el índice de la variable(**array**) donde la guardemos.
# Funciones utilizadas

outputJson : 
|  Nombre| Localización | Función 
|------------|------------|------------
| outputJson | jp_helper | retorna variables en formato JSON
