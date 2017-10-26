<?php

/**
* @author 	olaiya segun
* @since 	Oct 2016 refactored June 2017
* 
*/

class DB  
{

	static function updateOrCreate($table = NULL, $data = NULL, $where = NULL)
	{
		$CI =& get_instance();
		if($where != NULL && is_array($where)){

			if($CI->db->get_where($table, $where)->num_rows() > 0)
				return $CI->db->where($where)->update($table, $data);

		}

		$CI->db->insert($table, $data);
		return $CI->db->insert_id();
		
	}

	static function create($table = NULL, $data = NULL)
	{
		$CI =& get_instance();

		$CI->db->insert($table, $data);
		return $CI->db->insert_id();
	}

	static function update($table = NULL, $where = NULL, $data = NULL)
	{
		$CI =& get_instance();
		if($CI->db->get_where($table, $where)->num_rows() > 0)
			return $CI->db->where($where)->update($table, $data);
	}

	static function get($table=NULL, $where=NULL, $orderfield=NULL, $ordercode=NULL, $limit=NULL, $offset=NULL)
	{

		$CI =& get_instance();
		if($orderfield != NULL && $ordercode != NULL)
			$CI->db->order_by($orderfield, $ordercode);

		if($limit > 0 && $offset >= 0)
			$CI->db->limit($limit, $offset);

		if($where != NULL && is_array($where))
			return $CI->db->get_where($table, $where)->result();

		return $CI->db->get($table)->result();
	}

	static function firstOrNew($table = NULL, $where = NULL)
	{
		$CI =& get_instance();
		$tuple = NULL;

		if($where != NULL && is_array($where))
			$tuple = $CI->db->get_where($table, $where)->row();

		if($tuple == NULL){

			foreach($CI->db->list_fields($table) as $row)
				$tuple[$row] = '';

			$tuple = (object)$tuple;
		}

		return $tuple;
	}

	static function first($table = NULL, $where = NULL)
	{
		$CI =& get_instance();
		if($where != NULL && is_array($where))
			return $CI->db->get_where($table, $where)->row();

		return NULL;
	}

	static function delete($table = NULL, $where = NULL)
	{
		$CI =& get_instance();
		return $CI->db->where($where)->delete($table);
	}

	static function has($table = NULL, $field = NULL, $value = NULL)
	{
		$CI =& get_instance();
		return $CI->db->get_where($table, [$field=>$value])->num_rows() > 0 ? true : false;
	}

	static function contains($table = NULL, $where = NULL)
	{
		$CI =& get_instance();
		return $CI->db->get_where($table, $where)->num_rows() > 0 ? true : false;
	}

	
	static function count($table = NULL, $where = NULL)
	{
		$CI =& get_instance();
		return $CI->db->get_where($table, $where)->num_rows();
	}

	static function sum($table = NULL, $field = NULL, $where = [])
	{
		$CI =& get_instance();
		return $CI->db->where($where)->select_sum($field, 'sum')->get($table)->result()[0]->sum;
	}

	static function max($table = NULL, $field = NULL, $where = [])
	{
		$CI =& get_instance();
		return $CI->db->where($where)->select_max($field, 'max')->get($table)->result()[0]->max;
	}

	static function min($table = NULL, $field = NULL, $where = [])
	{
		$CI =& get_instance();
		return $CI->db->where($where)->select_max($field, 'min')->get($table)->result()[0]->min;
	}

	static function search($table = NULL, $field = NULL, $value = NULL, $count = FALSE, $side = 'both')
	{
		$CI =& get_instance();
		if(!$count)
			return $CI->db->like($field, $value, $side)->get($table)->result();

		return $CI->db->like($field, $value, $side)->get($table)->num_rows();

	}
	
}
