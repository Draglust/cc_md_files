# Diferentes tipos de llamada

> $this->load->library(['validation/validationValidations' , 'form_validation' ]);
> \$this->form_validation->validateData( \$data, \$rules)
> *Importante comprobar **mayúsculas / minúsculas**

> \$this->config->load('validation/'.ENVIRONMENT.'/config'  );
> $this->load->service("validation/validation_service");
> $this->load->model('loan/loan_aux_model');